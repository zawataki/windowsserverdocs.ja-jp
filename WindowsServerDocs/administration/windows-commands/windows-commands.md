---
title: Windows コマンド
description: Windows コマンド
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/26/2019
ms.prod: windows-server
ms.openlocfilehash: 5cb26bcff99d9cf3a1ee8b3a937ad6098a913c3d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362060"
---
# <a name="windows-commands"></a>Windows のコマンド

サポートされているすべてのバージョンの Windows (サーバーとクライアント) には、に組み込まれている一連の Win32 コンソールコマンドがあります。

この一連のドキュメントでは、スクリプトまたはスクリプトツールを使用してタスクを自動化するために使用できる Windows コマンドについて説明します。

特定のコマンドに関する情報を検索するには、次の A-Z メニューで、コマンドの開始文字をクリックし、コマンド名をクリックします。

[A](#a) |
[B](#b) | 
[C](#c) | 
[D](#d) | 
[E](#e) | 
[F](#f)1[G](#g)3[H](#h)5[I](#i)7[J](#j)9[K](#k)1[L](#l)3[M](#m)5[N](#n)7[O](#o)9[P](#p)1[Q](#q)3[R](#r)5[S](#s)7[T](#t)9[U](#u)1[V](#v)3[W](#w)5[X](#x) |Y |方向

## <a name="prerequisites"></a>前提条件

このトピックに記載されている情報は、以下に適用されます。

-   Windows Server 2019
-   Windows Server (半期チャネル)
-   Windows Server 2016
-   Windows Server 2012 R2
-   Windows Server 2012 
-   Windows Server 2008 R2
-   Windows Server 2008
-   Windows 10
-   Windows 8.1

### <a name="command-shell-overview"></a>コマンド シェルの概要

コマンドシェルは、ユーザーアカウント管理や夜間バックアップなどの日常的なタスクをバッチ (.bat) ファイルで自動化するために Windows に組み込まれた最初のシェルでした。 Windows スクリプトホストを使用すると、コマンドシェルでより高度なスクリプトを実行できます。 詳細については、「 [cscript](cscript.md)または[wscript](wscript.md)」を参照してください。 ユーザーインターフェイスを使用する場合よりも、スクリプトを使用すると操作をより効率的に実行できます。 スクリプトは、コマンドラインで使用可能なすべてのコマンドを受け入れます。

Windows には、次の2つのコマンドシェルがあります。コマンドシェルと[PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)。 各シェルは、ユーザーとオペレーティングシステムまたはアプリケーションとの直接通信を提供するソフトウェアプログラムであり、IT 運用を自動化するための環境を提供します。

PowerShell は、コマンドシェルの機能を拡張して、コマンドレットと呼ばれる PowerShell コマンドを実行するように設計されています。 コマンドレットは Windows コマンドに似ていますが、より拡張可能なスクリプト言語を提供します。 Powershell では Windows コマンドと PowerShell コマンドレットを実行できますが、コマンドシェルで実行できるのは PowerShell コマンドレットではなく Windows コマンドだけです。

最も堅牢で最新の Windows オートメーションの場合は、windows コマンドや windows スクリプトホストの代わりに PowerShell を使用することをお勧めします。 
> [!NOTE]
>Powershell のオープンソースバージョンである[Powershell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)をダウンロードしてインストールすることもできます。 

> [!CAUTION]
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリに次の変更を加える前に、コンピューター上の重要なデータをバックアップする必要があります。

> [!NOTE]
> コンピューターまたはユーザーのログオンセッションでコマンドシェルのファイル名とディレクトリ名の入力候補を有効または無効にするには、 **regedit.exe**を実行し、次の**reg_DWOrd 値**を設定します。
> 
> HKEY_LOCAL_MACHINE\Software\Microsoft\Command のプロセッサ名 (_e)
> 
> **Reg_DWOrd**値を設定するには、特定の関数に対して制御文字の16進値を使用します (たとえば、 **0 9**は Tab、 **0 08**は Backspace です)。 ユーザー指定の設定はコンピューターの設定よりも優先され、コマンドラインオプションはレジストリ設定よりも優先されます。

## <a name="command-line-reference-a-z"></a>コマンドラインリファレンス A-z

特定の Windows コマンドに関する情報を検索するには、次の A-Z メニューで、コマンドの開始文字をクリックし、コマンド名をクリックします。

[A](#a) |
[B](#b) | 
[C](#c) | 
[D](#d) | 
[E](#e) | 
[F](#f)1[G](#g)3[H](#h)5[I](#i)7[J](#j)9[K](#k)1[L](#l)3[M](#m)5[N](#n)7[O](#o)9[P](#p)1[Q](#q)3[R](#r)5[S](#s)7[T](#t)9[U](#u)1[V](#v)3[W](#w)5[X](#x) |Y |方向

### <a name="a"></a>A
-   [append](append.md)
-   [arp](arp.md)
-   [assoc](assoc.md)
-   [at](at.md)
-   [atmadm](atmadm.md)
-   [attrib](attrib.md)
-   [auditpol](auditpol.md)
-   [autochk](autochk.md)
-   [autoconv](autoconv.md)
-   [autofmt](autofmt.md)

### <a name="b"></a>B
- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
- [bitsadmin](bitsadmin.md)
  -   [bitsadmin addfile](bitsadmin-addfile.md)
  -   [bitsadmin addfileset](bitsadmin-addfileset.md)
  -   [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  -   [bitsadmin cancel](bitsadmin-cancel.md)
  -   [bitsadmin complete](bitsadmin-complete.md)
  -   [bitsadmin create](bitsadmin-create.md)
  -   [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  -   [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  -   [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  -   [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  -   [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  -   [bitsadmin getdescription](bitsadmin-getdescription.md)
  -   [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  -   [bitsadmin geterror](bitsadmin-geterror.md)
  -   [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  -   [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  -   [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  -   [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  -   [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  -   [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  -   [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  -   [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  -   [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  -   [bitsadmin getowner](bitsadmin-getowner.md)
  -   [bitsadmin の優先順位を取得する](bitsadmin-getpriority.md)
  -   [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  -   [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  -   [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  -   [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  -   [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  -   [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  -   [bitsadmin getstate](bitsadmin-getstate.md)
  -   [bitsadmin gettype](bitsadmin-gettype.md)
  -   [bitsadmin help](bitsadmin-help.md)
  -   [bitsadmin info](bitsadmin-info.md)
  -   [bitsadmin list](bitsadmin-list.md)
  -   [bitsadmin listfiles](bitsadmin-listfiles.md)
  -   [bitsadmin monitor](bitsadmin-monitor.md)
  -   [bitsadmin nowrap](bitsadmin-nowrap.md)
  -   [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  -   [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  -   [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  -   [bitsadmin reset](bitsadmin-reset.md)
  -   [bitsadmin resume](bitsadmin-resume.md)
  -   [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  -   [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  -   [bitsadmin setdescription](bitsadmin-setdescription.md)
  -   [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  -   [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  -   [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  -   [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  -   [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  -   [bitsadmin setpriority](bitsadmin-setpriority.md)
  -   [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  -   [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  -   [bitsadmin suspend](bitsadmin-suspend.md)
  -   [bitsadmin takeownership](bitsadmin-takeownership.md)
  -   [bitsadmin 転送](bitsadmin-transfer.md)
  -   [bitsadmin util](bitsadmin-util.md)
  -   [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  -   [bootcfg addsw](bootcfg-addsw.md)
  -   [bootcfg copy](bootcfg-copy.md)
  -   [bootcfg dbg1394](bootcfg-dbg1394.md)
  -   [bootcfg debug](bootcfg-debug.md)  
  -   [bootcfg default](bootcfg-default.md)
  -   [bootcfg delete](bootcfg-delete.md)
  -   [bootcfg ems](bootcfg-ems.md)
  -   [bootcfg query](bootcfg-query.md)
  -   [bootcfg raw](bootcfg-raw.md)
  -   [bootcfg rmsw](bootcfg-rmsw.md)
  -   [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>c
- [cacls](cacls_1.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  -   [change logon](change-logon.md)
  -   [change port](change-port.md)
  -   [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir_1.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [Cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [convert](convert.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [cscript](cscript.md)

### <a name="d"></a>D
-   [date](date.md)
-   [dcgpofix](dcgpofix.md)
-   [defrag](defrag.md)
-   [del](del.md)
-   [dfsrmig](dfsrmig.md)
-   [diantz](diantz.md)
-   [dir](dir.md)
-   [diskcomp](diskcomp.md)
-   [diskcopy](diskcopy.md)
-   [diskpart](diskpart.md)
-   [diskperf](diskperf.md)
-   [diskraid](diskraid.md)
-   [diskshadow](diskshadow.md)
-   [dispdiag](dispdiag.md)
-   [あるいは](Dnscmd.md)
-   [doskey](doskey.md)
-   [driverquery](driverquery.md)

### <a name="e"></a>E
-   [echo](echo.md)
-   [edit](edit.md)
-   [endlocal](endlocal.md)
-   [erase](erase.md)
-   [eventcreate](eventcreate.md)
-   [eventquery](eventquery.md)
-   [eventtriggers](eventtriggers.md)
-   [evntcmd](Evntcmd.md)
-   [exit](exit_2.md)
-   [expand](expand.md)
-   [extract](extract.md)

### <a name="f"></a>F
- [fc](fc.md)
- [find](find.md)
- [findstr](findstr.md)
- [finger](finger.md)
- [flattemp](flattemp.md)
- [fondue](fondue.md)
- [for](for.md)
- [forfiles](forfiles.md)
- [format](format.md)
- [freedisk](freedisk.md)
- [fsutil](fsutil.md)
  -   [fsutil 8dot3name](fsutil-8dot3name.md) 
  -   [fsutil behavior](fsutil-behavior.md) 
  -   [fsutil file](fsutil-file.md)
  -   [fsutil fsinfo](fsutil-fsinfo.md)
  -   [fsutil hardlink](fsutil-hardlink.md)
  -   [fsutil objectid](fsutil-objectid.md)
  -   [fsutil quota](fsutil-quota.md)
  -   [fsutil repair](fsutil-repair.md)
  -   [fsutil reparsepoint](fsutil-reparsepoint.md)
  -   [fsutil resource](fsutil-resource.md)
  -   [fsutil sparse](fsutil-sparse.md)
  -   [fsutil tiering](fsutil-tiering.md)
  -   [fsutil transaction](fsutil-transaction.md)
  -   [fsutil usn](fsutil-usn.md)
  -   [fsutil volume](fsutil-volume.md)
  -   [fsutil wim](fsutil-wim.md)
- [パッシブ](ftp.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G
-   [getmac](getmac.md)
-   [gettype](gettype.md)
-   [goto](goto.md)
-   [gpfixup](gpfixup.md)
-   [gpresult](gpresult.md)
-   [gpupdate](gpupdate.md)
-   [graftabl](graftabl.md)

### <a name="h"></a>H
-   [help](help.md)
-   [helpctr](helpctr.md)
-   [hostname](hostname.md)

### <a name="i"></a>I
-   [icacls](icacls.md)
-   [if](if.md)
-   [inuse](inuse.md)
-   [ipconfig](ipconfig.md)
-   [ipxroute](ipxroute.md)
-   [irftp](irftp.md)

### <a name="j"></a>J
-   [jetpack](jetpack.md)

### <a name="k"></a>K
- [klist](klist.md)
- [ksetup](ksetup.md)
  -   [ksetup: setrealm](ksetup-setrealm.md)
  -   [ksetup: mapuser](ksetup-mapuser.md)
  -   [ksetup: addkdc](ksetup-addkdc.md)
  -   [ksetup: delkdc](ksetup-delkdc.md)
  -   [ksetup: addkpasswd](ksetup-addkpasswd.md)
  -   [ksetup: delkpasswd](ksetup-delkpasswd.md)
  -   [ksetup: サーバー](ksetup-server.md)
  -   [ksetup: setcomputerpassword](ksetup-setcomputerpassword.md)
  -   [ksetup: removerealm](ksetup-removerealm.md)
  -   [ksetup: ドメイン](ksetup-domain.md)
  -   [ksetup: changepassword](ksetup-changepassword.md)
  -   [ksetup: listrealmflags](ksetup-listrealmflags.md)
  -   [ksetup: setrealmflags](ksetup-setrealmflags.md)
  -   [ksetup: addrealmflags](ksetup-addrealmflags.md)
  -   [ksetup: delrealmflags](ksetup-delrealmflags.md)
  -   [ksetup: dumpstate](ksetup-dumpstate.md)
  -   [ksetup: addhost almmap](ksetup-addhosttorealmmap.md)
  -   [ksetup: delhost almmap](ksetup-delhosttorealmmap.md)
  -   [ksetup: setenctypeattr](ksetup-setenctypeattr.md)
  -   [ksetup: getenctypeattr](ksetup-getenctypeattr.md)
  -   [ksetup: addenctypeattr](ksetup-addenctypeattr.md)
  -   [ksetup: delenctypeattr](ksetup-delenctypeattr.md) 
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L
- [label](label.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  -   [logman create](logman-create.md)
  -   [logman query](logman-query.md)
  -   [logman 開始 & 124;停止](logman-start-stop.md)
  -   [logman delete](logman-delete.md)
  -   [logman update](logman-update.md)
  -   [logman インポート & 124;輸出](logman-import-export.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M
- [macfile](macfile.md)
- [makecab](makecab.md)
- [manage-bde](manage-bde.md)
  -   [manage-bde: 状態](manage-bde-status.md)
  -   [manage-bde: on](manage-bde-on.md)
  -   [manage-bde: off](manage-bde-off.md)
  -   [manage-bde: pause](manage-bde-pause.md)
  -   [manage-bde: resume](manage-bde-resume.md)
  -   [manage-bde: lock](manage-bde-lock.md)
  -   [manage-bde: unlock](manage-bde-unlock.md)
  -   [manage-bde: 自動ロック解除](manage-bde-autounlock.md)
  -   [manage-bde: プロテクター](manage-bde-protectors.md)
  -   [manage-bde: tpm](manage-bde-tpm.md)
  -   [manage-bde: setidentifier](manage-bde-setidentifier.md)
  -   [manage:ForceRecovery](manage-bde-forcerecovery.md)
  -   [manage-bde: changepassword](manage-bde-changepassword.md)
  -   [manage-bde: changepin](manage-bde-changepin.md)
  -   [manage-bde: 変更キー](manage-bde-changekey.md)
  -   [manage:KeyPackage](manage-bde-keypackage.md)
  -   [manage-bde: upgrade](manage-bde-upgrade.md)
  -   [manage:WipeFreeSpace](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [Md](Md.md)
- [mkdir](mkdir.md)
- [mklink](mklink.md)
- [mmc](mmc.md)
- [mode](mode.md)
- [more](more.md)
- [mount](mount.md)
- [mountvol](mountvol.md)
- [move](move.md)
- [mqbkup](mqbkup.md)
- [mqsvc](mqsvc.md)
- [mqtgsvc](mqtgsvc.md)
- [msdt](msdt.md)
- [msg](msg.md)
- [msiexec](msiexec.md)
- [msinfo32](msinfo32.md)
- [mstsc](mstsc.md)

### <a name="n"></a>N
- [nbtstat](nbtstat.md)
- [netcfg](netcfg.md)
- [netsh](netsh.md)
- [netstat](netstat.md)
- [Net print](net-print.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  -   [nslookup exit コマンド](nslookup-exit-command.md)
  -   [nslookup finger コマンド](nslookup-finger-command.md)
  -   [nslookup help](nslookup-help.md)
  -   [nslookup ls](nslookup-ls.md)
  -   [nslookup lserver](nslookup-lserver.md)
  -   [nslookup root](nslookup-root.md)
  -   [nslookup server](nslookup-server.md)
  -   [nslookup set](nslookup-set.md)
  -   [nslookup set all](nslookup-set-all.md)
  -   [nslookup set class](nslookup-set-class.md)
  -   [nslookup set d2](nslookup-set-d2.md)
  -   [nslookup set debug](nslookup-set-debug.md)
  -   [nslookup set domain](nslookup-set-domain.md)
  -   [nslookup set port](nslookup-set-port.md)
  -   [nslookup set querytype](nslookup-set-querytype.md)
  -   [nslookup set recurse](nslookup-set-recurse.md)
  -   [nslookup set retry](nslookup-set-retry.md)
  -   [nslookup set root](nslookup-set-root.md)
  -   [nslookup set search](nslookup-set-search.md)
  -   [nslookup set srchlist](nslookup-set-srchlist.md)
  -   [nslookup set timeout](nslookup-set-timeout.md)
  -   [nslookup set type](nslookup-set-type.md)
  -   [nslookup set vc](nslookup-set-vc.md)
  -   [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O
-   [openfiles](openfiles.md)

### <a name="p"></a>P
-   [pagefileconfig](pagefileconfig.md)
-   [path](path.md)
-   [pathping](pathping.md)
-   [pause](pause.md)
-   [pbadmin](pbadmin.md)
-   [pentnt](pentnt.md)
-   [perfmon](perfmon.md)
-   [ping](ping.md)
-   [pnpunattend](pnpunattend.md)
-   [pnputil](pnputil.md)
-   [popd](popd.md)
-   [PowerShell](PowerShell.md)
-   [PowerShell_ise](PowerShell_ise.md)
-   [print](print.md)
-   [prncnfg](prncnfg.md)
-   [prndrvr](prndrvr.md)
-   [prnjobs](prnjobs.md)
-   [prnmngr](prnmngr.md)
-   [prnport](prnport.md)
-   [prnqctl](prnqctl.md)
-   [prompt](prompt.md)
-   [pubprn](pubprn.md)
-   [pushd](pushd.md)
-   [pushprinterconnections](pushprinterconnections.md)

### <a name="q"></a>Q
-   [qappsrv](qappsrv.md)
-   [qprocess](qprocess.md)
-   [query](query.md)
-   [quser](quser.md)
-   [qwinsta](qwinsta.md)

### <a name="r"></a>R
- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [reg](reg.md)
  -   [reg add](reg-add.md)
  -   [reg 比較](reg-compare.md)
  -   [reg コピー](reg-copy.md)
  -   [reg の削除](reg-delete.md)
  -   [reg エクスポート](reg-export.md)
  -   [reg インポート](reg-import.md)
  -   [reg 読み込み](reg-load.md)
  -   [reg クエリ](reg-query.md)
  -   [reg 復元](reg-restore.md)
  -   [reg 保存](reg-save.md)
  -   [reg アンロード](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [rem](rem.md)
- [ren](ren.md)
- [rename](rename.md)
- [repair-bde](repair-bde.md)
- [replace](replace.md)
- [reset session](reset-session.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [route_ws2008](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>S
- [schtasks](schtasks.md)
- [scwcmd](Scwcmd.md)
  -   [scwcmd: 分析](scwcmd-analyze.md)
  -   [scwcmd: 構成](scwcmd-configure.md)
  -   [scwcmd: 登録](scwcmd-register.md) 
  -   [scwcmd: ロールバック](scwcmd-rollback.md) 
  -   [scwcmd: transform](scwcmd-transform.md) 
  -   [scwcmd: 表示](scwcmd-view.md) 
- [secedit](secedit.md)
  -   [secedit: 分析](secedit-analyze.md)
  -   [secedit: 構成](secedit-configure.md)
  -   [secedit: エクスポート](secedit-export.md)
  -   [secedit: generaterollback](secedit-generaterollback.md)
  -   [secedit: インポート](secedit-import.md)
  -   [secedit: validate](secedit-validate.md)
- [serverceipoptin](serverceipoptin.md)
- [Servermanagercmd](Servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [set](set_1.md)
- [setlocal](setlocal.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [shutdown](shutdown.md)
- [sort](sort.md)
- [start](start.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)

### <a name="t"></a>T
-   [takeown](takeown.md)
-   [tapicfg](tapicfg.md)
-   [taskkill](taskkill.md)
-   [tasklist](tasklist.md)
-   [tcmsetup](tcmsetup.md)
-   [telnet](telnet.md)
-   [tftp](tftp.md)
-   [time](time.md)
-   [timeout](timeout_1.md)
-   [title](title_1.md)
-   [tlntadmn](tlntadmn.md)
-   [tpmvscmgr](tpmvscmgr.md)
-   [tracerpt](tracerpt_1.md)
-   [tracert](tracert.md)
-   [tree](tree.md)
-   [tscon](tscon.md)
-   [tsdiscon](tsdiscon.md)
-   [tsecimp](tsecimp_1.md)
-   [tskill](tskill.md)
-   [tsprof](tsprof.md)
-   [type](type.md)
-   [typeperf](typeperf.md)
-   [tzutil](tzutil.md)

### <a name="u"></a>U
-   [unlodctr](unlodctr_1.md)

### <a name="v"></a>V
-   [ver](ver.md)
-   [verifier](verifier.md)
-   [verify](verify_1.md)
-   [vol](vol.md)
-   [vssadmin](vssadmin.md)- 

### <a name="w"></a>W
- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  -   [wbadmin のバックアップの有効化](wbadmin-enable-backup.md)
  -   [wbadmin のバックアップの無効化](wbadmin-disable-backup.md)
  -   [wbadmin のバックアップの開始](wbadmin-start-backup.md)
  -   [wbadmin 停止ジョブ](wbadmin-stop-job.md)
  -   [wbadmin get のバージョン](wbadmin-get-versions.md)
  -   [wbadmin の項目の取得](wbadmin-get-items.md)
  -   [wbadmin の回復の開始](wbadmin-start-recovery.md)
  -   [wbadmin の状態の取得](wbadmin-get-status.md)
  -   [wbadmin のディスクの取得](wbadmin-get-disks.md)
  -   [wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  -   [wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)
  -   [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  -   [wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)
  -   [wbadmin restore カタログ](wbadmin-restore-catalog.md)
  -   [wbadmin delete カタログ](wbadmin-delete-catalog.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [wlbs.exe](wlbs_1.md)
- [wmic](wmic.md)
- [wscript](wscript.md)

### <a name="x"></a>x
-   [xcopy](xcopy.md)
