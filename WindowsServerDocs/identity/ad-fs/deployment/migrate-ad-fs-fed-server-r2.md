---
title: AD FS 2.0 フェデレーション サーバーを移行します。
description: Windows Server 2012 R2 への AD FS サーバーの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46d0b643d786443093e0dfeafe4cddde3278ff76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444623"
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>AD FS 2.0 フェデレーション サーバーを Windows Server 2012 R2 で AD FS に移行します。

単一ノード AD FS ファーム、WIF ファーム、または Windows Server 2012 R2 の SQL Server ファームに属している AD FS フェデレーション サーバーを移行するには、次のタスクを実行する必要があります。  
  
1.  [エクスポートし、AD FS 構成データのバックアップ](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Windows Server 2012 R2 AD FS ファームへのインポート元の構成データ](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>AD FS 構成データをエクスポートおよびバックアップする  
 AD FS の構成設定をエクスポートするには、次の手順を実行します。  
  
###  <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには  
  
1.  .pfx ファイル内の次の証明書とそれらの秘密キーにアクセスできることを確認します。  
  
    -   移行するフェデレーション サーバー ファームで使用される SSL 証明書  
  
    -   移行するフェデレーション サーバー ファームで使用されるサービス通信証明書 (SSL 証明書と異なる場合)  
  
    -   移行するフェデレーション サーバー ファームで使用されるすべてのサード パーティのトークン署名証明書またはトークン暗号化/暗号化解除証明書  
  
SSL 証明書を検索するには、インターネット インフォメーション サービス (IIS) 管理コンソールを開き、左ウィンドウで **[既定の Web サイト]** を選択します。 **[操作]** **アクション**ペイン、検索、および https バインドを選択します をクリックして**編集**、 をクリックし、**ビュー**します。  
  
フェデレーション サービスによって使用される SSL 証明書とその秘密キーを .pfx ファイルにエクスポートする必要があります。 詳細については、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](export-the-private-key-portion-of-a-server-authentication-certificate.md)を参照してください。  
  
> [!NOTE]
>  Windows Server 2012 R2 で AD FS の実行の一部としてデバイス登録サービスをデプロイする場合は、新しい SSL 証明書を取得する必要があります。詳細については、「[AD FS の SSL 証明書を登録する](enroll-an-ssl-certificate-for-ad-fs.md)」と「[デバイス登録サービスを使用してフェデレーション サーバーを構成する](configure-a-federation-server-with-device-registration-service.md)」を参照してください。  
  
使用中のトークン署名証明書、トークン暗号化証明書、サービス通信証明書を表示するには、次の Windows PowerShell コマンドを実行して、使用中のすべての証明書のリストをファイル内に作成します。  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2. AD FS フェデレーション サービスのプロパティ (フェデレーション サービス名、フェデレーション サービス表示名、フェデレーション サーバー識別子など) をファイルにエクスポートします。  
  
フェデレーション サービスのプロパティをエクスポートするには、Windows PowerShell を開き、 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

出力ファイルには次の重要な構成値が含まれます。  
 
|**Get-adfsproperties によって報告された、フェデレーション サービスのプロパティ名**|**AD FS 管理コンソールで、フェデレーション サービスのプロパティ名**|
|-----|-----|  
|HostName|フェデレーション サービス名|  
|識別子|フェデレーション サービスの識別子|  
|DisplayName|フェデレーション サービスの表示名|  
  
3. アプリケーション構成ファイルをバックアップします。 その他の設定として、このファイルにはポリシー データベースの接続文字列が含まれます。  
  
アプリケーション構成ファイルをバックアップするには、 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` ファイルをバックアップ サーバーの安全な場所に手動でコピーする必要があります。  
  
> [!NOTE]
>  このファイル内で "policystore connectionstring=" の直後にあるデータベース接続文字列をメモしてください。 接続文字列で SQL Server データベースが指定されている場合、フェデレーション サーバーで元の AD FS 構成を復元するときに、この値が必要になります。  
>   
>  たとえば、WID 接続文字列は `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"` となります。 SQL Server 接続文字列は `"Data Source=databasehostname;Integrated Security=True"` となります。  
  
4. AD FS フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。  
  
ID 値を検索するには、 **[サービス]** コンソールで **[AD FS 2.0 Windows サービス]** の **[ログオン方法]** 列を調べ、この値を手動で記録します。  
  
> [!NOTE]
>  スタンドアロン フェデレーション サービスの場合、組み込みのネットワーク サービス アカウントが使用されます。  この場合、パスワードは必要ありません。  
  
5. 有効な AD FS エンドポイントのリストをファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6. カスタム要求記述をファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7. web.config ファイルで構成されている useRelayStateForIdpInitiatedSignOn などのカスタム設定がある場合は、参照用に web.config ファイルをバックアップしてください。 IIS で仮想パス **"/adfs/ls"** にマップされているディレクトリからこのファイルをコピーできます。 既定では、そのファイルは **%systemdrive%\inetpub\adfs\ls** ディレクトリにあります。  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>要求プロバイダー信頼と証明書利用者信頼をエクスポートするには  
  
1.  FS の要求プロバイダー信頼を AD にエクスポートして、パーティの信頼関係証明書利用者、する必要があります管理者としてログイン (ただし、ドメイン管理者としてされません) フェデレーション サーバーと、次の Windows PowerShell のスクリプトは実行に配置されて、**メディア/server_support/adfs** 、Windows Server 2012 R2 のインストール CD のフォルダー:`export-federationconfiguration.ps1`します。  
  
> [!IMPORTANT]
>  エクスポート スクリプトは次のパラメーターを受け取ります。  
> 
> - Export-FederationConfiguration.ps1 -Path <string\> [-ComputerName <string\>] [-Credential <pscredential\>] [-Force] [-CertificatePassword <securestring\>]  
>   -   エクスポート FederationConfiguration.ps1-パス < 文字列\>[-ComputerName < 文字列\>] [-資格情報 < pscredential\>] [-Force] [-CertificatePassword < securestring\>] [-RelyingPartyTrustIdentifier < string[] >] [-ClaimsProviderTrustIdentifier < string[] >]  
>   -   エクスポート FederationConfiguration.ps1-パス < 文字列\>[-ComputerName < 文字列\>] [-資格情報 < pscredential\>] [-Force] [-CertificatePassword < securestring\>] [-RelyingPartyTrustName < string[] >] [-ClaimsProviderTrustName < string[] >]  
> 
>   **-RelyingPartyTrustIdentifier <string[]>** - このコマンドレットは、識別子が string 配列に指定されている証明書利用者信頼のみをエクスポートします。 既定では、どの証明書利用者信頼もエクスポートしません。 RelyingPartyTrustIdentifier、ClaimsProviderTrustIdentifier、RelyingPartyTrustName、および ClaimsProviderTrustName のいずれも指定されていない場合、このスクリプトはすべての証明書利用者信頼と要求プロバイダー信頼をエクスポートします。  
> 
>   **-ClaimsProviderTrustIdentifier <string[]>** - このコマンドレットは、識別子が string 配列に指定されている要求プロバイダー信頼のみをエクスポートします。 既定では、どの要求プロバイダー信頼もエクスポートしません。  
> 
>   **-RelyingPartyTrustName <string[]>** - このコマンドレットは、名前が string 配列に指定されている証明書利用者信頼のみをエクスポートします。 既定では、どの証明書利用者信頼もエクスポートしません。  
> 
>   **-ClaimsProviderTrustName <string[]>** - このコマンドレットは、名前が string 配列に指定されている要求プロバイダー信頼のみをエクスポートします。 既定では、どの要求プロバイダー信頼もエクスポートしません。  
> 
>   **-Path < 文字列\>** -エクスポートされたファイルが含まれるフォルダーへのパス。  
> 
>   **-ComputerName < 文字列\>** -STS サーバーのホスト名を指定します。 既定はローカル コンピュータです。 AD FS 2.0 または Windows Server 2012 の AD FS を Windows Server 2012 R2 の AD FS に移行する場合、これはレガシ AD FS サーバーのホスト名です。  
> 
>   **-Credential < PSCredential\>**  -この操作を実行する権限を持つユーザー アカウントを指定します。 既定値は現在のユーザーです。  
> 
>   **-Force** – ユーザーの確認を求めないように指定します。  
> 
>   **-Certificatepassword < SecureString\>**  -AD FS 証明書の秘密キーをエクスポートするためのパスワードを指定します。 指定しない場合、AD FS の証明書と秘密キーをエクスポートする必要があるときに、スクリプトはパスワードの入力を求めます。  
> 
>   **入力**:なし  
> 
>   **出力**: string - このコマンドレットはエクスポート フォルダーのパスを返します。 返されたオブジェクトを Import-FederationConfiguration にパイプで渡すことができます。  
  
###  <a name="to-back-up-custom-attribute-stores"></a>カスタム属性ストアをバックアップするには  
  
1.  Windows Server 2012 R2 で新しい AD FS ファームに維持するすべてのカスタム属性ストアを手動でエクスポートする必要があります。  
  
> [!NOTE]
>  Windows Server 2012 R2 で AD FS に .NET Framework 4.0 以降に基づいているカスタム属性ストアが必要です。 [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) の手順に従って、.Net Framework 4.5 をインストールして設定してください。  
  
AD FS によって使用中のカスタム属性ストアについて情報を検索するには、Windows PowerShell コマンド 

``` powershell
Get-ADFSAttributeStore
```  

カスタム属性ストアのアップグレードまたは移行手順はさまざまです。  
  
2. Windows Server 2012 R2 で新しい AD FS ファームに維持するカスタム属性ストアのすべての .dll ファイルを手動でエクスポートする必要があります。 カスタム属性ストアの .dll ファイルのアップグレードまたは移行手順はさまざまです。  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Windows Server 2012 R2 フェデレーション サーバー ファームを作成する  
  
1.  フェデレーション サーバーとして機能し、AD FS サーバーの役割を追加するコンピューターで Windows Server 2012 R2 のオペレーティング システムをインストールします。 詳細については、「[AD FS 役割サービスをインストールする](install-the-ad-fs-role-service.md)」を参照してください。 その後、Active Directory フェデレーション サービス構成ウィザードまたは Windows PowerShell のいずれかを使用して、新しいフェデレーション サービスを構成します。 詳細については、「[フェデレーション サーバーを構成する](configure-a-federation-server.md)」の「新しいフェデレーション サーバー ファームの最初のフェデレーション サーバーを構成する」を参照してください。  

この手順の実行中、次の指示に従う必要があります。  
  
-   フェデレーション サービスを構成するために、Domain Administrator の特権が必要です。  
  
-   AD FS 2.0 または Windows Server 2012 の AD FS で使用していた同じフェデレーション サービス名 (ファーム名) を使用する必要があります。 同じフェデレーション サービス名を使用しない場合、構成しようとしている Windows Server 2012 R2 フェデレーション サービスでバックアップした証明書は機能しません。  
  
-   このフェデレーション サーバー ファームが WID ファームか SQL Server ファームかを指定します。 SQL Server ファームの場合、SQL Server データベースの場所とインスタンス名を指定します。  
  
-   AD FS の移行プロセスの準備中にバックアップした SSL サーバー認証証明書を含む、pfx ファイルを指定する必要があります。  
  
-   AD FS 2.0 または Windows Server 2012 ファーム内の AD FS で使用していた同じサービス アカウント ID を指定する必要があります。  
  
2. 最初のノードが構成されたら、その他のノードを新しいファームに追加できます。 詳細については、「[フェデレーション サーバーを構成する](configure-a-federation-server.md)」の「フェデレーション サーバーを既存のフェデレーション サーバー ファームに追加する」を参照してください。  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>元の構成データを Windows Server 2012 R2 の AD FS ファームにインポートする  
 Windows Server 2012 R2 で実行されている AD FS フェデレーション サーバー ファームを作成したので、そこに元の AD FS 構成データをインポートできます。  
  
1.  その他のカスタム AD FS 証明書をインポートして構成します。たとえば、外部で登録したトークン署名証明書とトークン暗号化/暗号化解除証明書のほか、サービス通信証明書 (SSL 証明書と異なる場合) などです。  
  
AD FS 管理コンソールで、 **[証明書]** を選択します。 サービス通信証明書、トークン暗号化/暗号化解除証明書、トークン署名証明書を確認するには、各証明書を、移行の準備中に certificates.txt ファイルにエクスポートした値と照合します。  
  
トークン暗号化解除証明書またはトークン署名証明書を既定の自己署名証明書から外部証明書に変更するには、まず、既定で有効になっている自動証明書ロールオーバー機能を無効にする必要があります。 これを行うには、Windows PowerShell の  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2. Set-AdfsProperties コマンドレットを使用して、AutoCertificateRollover や SSO 有効期間など、AD FS サービスのカスタム設定をすべて構成します。  
  
3. AD FS 証明書利用者の信頼と要求プロバイダー信頼をインポートするには、管理者としてログインする必要があります (ただし、ドメイン管理者としていない) サーバーと、次の Windows PowerShell のスクリプトは実行で \support\adfs フォルダーにあるフェデレーションWindows Server 2012 R2 のインストール CD。  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  インポート スクリプトは次のパラメーターを受け取ります。  
> 
> - Import-FederationConfiguration.ps1 -Path <string\> [-ComputerName <string\>] [-Credential <pscredential\>] [-Force] [-LogPath <string\>] [-CertificatePassword <securestring\>]  
>   -   インポート FederationConfiguration.ps1-パス < 文字列\>[-ComputerName < 文字列\>] [-資格情報 < pscredential\>] [-Force] [-LogPath < 文字列\>] [-CertificatePassword < securestring\>] [-RelyingPartyTrustIdentifier < string[] >] [-ClaimsProviderTrustIdentifier < string[] >  
>   -   インポート FederationConfiguration.ps1-パス < 文字列\>[-ComputerName < 文字列\>] [-資格情報 < pscredential\>] [-Force] [-LogPath < 文字列\>] [-CertificatePassword < securestring\>] [-RelyingPartyTrustName < string[] >] [-ClaimsProviderTrustName < string[] >]  
> 
>   **-RelyingPartyTrustIdentifier <string[]>** - このコマンドレットは、識別子が string 配列に指定されている証明書利用者信頼のみをインポートします。 既定では、どの証明書利用者信頼もインポートしません。 RelyingPartyTrustIdentifier、ClaimsProviderTrustIdentifier、RelyingPartyTrustName、および ClaimsProviderTrustName のいずれも指定されていない場合、このスクリプトはすべての証明書利用者信頼と要求プロバイダー信頼をインポートします。  
> 
>   **-ClaimsProviderTrustIdentifier <string[]>** - このコマンドレットは、識別子が string 配列に指定されている要求プロバイダー信頼のみをインポートします。 既定では、どの要求プロバイダー信頼もインポートしません。  
> 
>   **-RelyingPartyTrustName <string[]>** - このコマンドレットは、名前が string 配列に指定されている証明書利用者信頼のみをインポートします。 既定では、どの証明書利用者信頼もインポートしません。  
> 
>   **-ClaimsProviderTrustName <string[]>** - このコマンドレットは、名前が string 配列に指定されている要求プロバイダー信頼のみをインポートします。 既定では、どの要求プロバイダー信頼もインポートしません。  
> 
>   **-Path < 文字列\>** -インポートする構成ファイルを含むフォルダーへのパス。  
> 
>   **-Logpath < 文字列\>** -インポート ログ ファイルを格納するフォルダーへのパス。 "import.log" という名前のログ ファイルがこのフォルダーに作成されます。  
> 
>   **-ComputerName < 文字列\>** -STS サーバーのホスト名を指定します。 既定はローカル コンピュータです。 AD FS 2.0 または Windows Server 2012 の AD FS を Windows Server 2012 R2 の AD FS に移行する場合、このパラメーターはレガシ AD FS サーバーのホスト名に設定する必要があります。  
> 
>   **-Credential < PSCredential\>** -この操作を実行する権限を持つユーザー アカウントを指定します。 既定値は現在のユーザーです。  
> 
>   **-Force** – ユーザーの確認を求めないように指定します。  
> 
>   **-Certificatepassword < SecureString\>**  -AD FS 証明書の秘密キーをインポートするためのパスワードを指定します。 指定しない場合、AD FS の証明書と秘密キーをインポートする必要があるときに、スクリプトはパスワードの入力を求めます。  
> 
>   **入力**: string - このコマンドは入力としてインポート フォルダーのパスを受け取ります。 Export-FederationConfiguration をパイプでこのコマンドに渡すことができます。  
> 
>   **出力:** なし。  
  
証明書利用者信頼の WSFedEndpoint プロパティの末尾にあるスペースは、インポート スクリプトのエラーの原因になることがあります。 この場合、インポート前にファイルからスペースを手動で削除します。 たとえば、次のエントリはエラーの原因になります。  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444 /</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83 /</URI>  
    ```  
  
     They must be edited to:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444/</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83/</URI>  
    ```  
> [!IMPORTANT]
>  ソース システムで Active Directory 要求プロバイダー信頼にカスタム要求規則 (AD FS の既定の規則以外の規則) がある場合、それらの規則はスクリプトによって移行されません。 Windows Server 2012 R2 は、新しい既定値を持つためにです。 新しい Windows Server 2012 R2 ファーム内の Active Directory 要求プロバイダー信頼に手動で追加するでは、カスタム規則はすべてをマージする必要があります。  
  
4. カスタム AD FS エンドポイントの設定をすべて構成します。 AD FS 管理コンソールで、 **[エンドポイント]** を選択します。 有効な AD FS エンドポイントを、AD FS の移行の準備中にファイルにエクスポートした有効な AD FS エンドポイントのリストと照合します。  
  
    \- -  
  
    カスタム要求記述をすべて構成します。 AD FS 管理コンソールで、 **[要求記述]** を選択します。 AD FS の要求記述のリストを、AD FS の移行の準備中にファイルにエクスポートした要求記述のリストと照合します。 ファイルに含まれるが AD FS の既定のリストに含まれないカスタム要求記述をすべて追加します。 管理コンソール内の要求識別子はファイル内の ClaimType にマップされることに注意してください。  
  
5. バックアップしたすべてのカスタム属性ストアをインストールして構成します。 管理者として、すべてのカスタム属性ストアのバイナリが .NET Framework 4.0 以上にアップグレードされていることを確認してから、それらの属性ストアを参照するように AD FS の構成を更新してください。  
  
6. レガシ web.config ファイル パラメーターにマップされているサービス プロパティを構成します。  
  
   -   場合**useRelayStateForIdpInitiatedSignOn**に追加された、 **web.config**ファイルの AD FS 2.0 または Windows Server 2012 ファーム内の AD FS での AD FS で次のサービス プロパティを構成する必要がありますWindows Server 2012 R2 ファーム:  
  
       -   Windows Server 2012 R2 で AD FS が含まれています、 **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config**ファイル。 同じ構文で要素を作成、 **web.config**ファイルの要素:`<useRelayStateForIdpInitiatedSignOn enabled="true" />`します。 一部としてこの要素を含める **< microsoft.identityserver.web >** のセクション、 **Microsoft.IdentityServer.Servicehost.exe.config**ファイル。  
  
   -   場合 **< persistIdentityProviderInformation を有効になっている ="true&#124;false"lifetimeInDays「90」enablewhrPersistence を = ="true&#124;false"/\>** に追加された、 **web.config**ファイルの AD fs 2.0 または AD FS ファームでは Windows Server 2012、Windows Server 2012 R2 ファームで AD FS で次のサービス プロパティを構成する必要があります。  
  
       1.  Windows Server 2012 R2 で AD FS で次の Windows PowerShell コマンドを実行します:`Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`します。  
  
   -   場合 **< シングル サインオンを有効になっている ="true&#124;false"/\>** に追加された、 **web.config**ファイルで、AD FS 2.0 または Windows Server 2012 ファーム内の AD FS は、追加のサービスを設定する必要はありませんWindows Server 2012 R2 ファーム内の AD fs のプロパティです。 シングル サインオンは、Windows Server 2012 R2 ファームで AD FS での既定で有効です。  
  
   -   LocalAuthenticationTypes 設定が追加された場合、 **web.config**ファイル、AD FS 2.0 または AD FS ファームでは Windows Server 2012、Windows Server 2012 R2 ファームで AD FS で次のサービス プロパティを構成する必要があります。  
  
       -   両方のフェデレーション サービスとプロキシの認証タイプをサポートするためにグローバル認証ポリシーの設定は、統合、Forms、TlsClient、Basic Transform の一覧で Windows Server 2012 R2 AD fs からが。 これらの設定は AD FS 管理スナップインの **[認証ポリシー]** で設定できます。  
  
   元の構成データのインポート後、必要に応じて AD FS サインイン ページをカスタマイズできます。 詳細については、「 [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービス役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)