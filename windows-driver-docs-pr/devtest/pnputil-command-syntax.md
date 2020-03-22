---
title: PnPUtil のコマンド構文
description: 構文とパラメーターを含む、PnPUtil を実行する方法。
ms.assetid: f14ceb98-8d82-43dd-b06e-2595b59b6999
keywords:
- PnPUtil コマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- PnPUtil
api_type:
- NA
ms.date: 03/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: 56d770e3b97ffe1ded69290f045b592bdd012a01
ms.sourcegitcommit: 4058fcb136cfb8255ca7bec68e8597c89f7b68cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80080155"
---
# <a name="pnputil-command-syntax"></a>PnPUtil のコマンド構文


PnPUtil を実行するには、コマンドプロンプトウィンドウを開き (**管理者として実行**)、次の構文とパラメーターを使用してコマンドを入力します。

**注**  PnPUtil (pnputil) は、windows Vista 以降 (% windir%\\system32 ディレクトリ内) のすべてのバージョンの windows に含まれています。

 

```
pnputil [/add-driver <...> | /delete-driver <...> |
         /export-driver <...> | /enum-drivers     |
     /disable-device <...> | /enable-device <...> |
     /restart-device <...> | /remove-device <...> | 
     /scan-devices <...> | /enum-devices <...>    |
     /enum-interfaces <...> | /?]
```

## <a name="commands"></a>コマンド

 **/add-driver** * < filename. inf | *.inf > [/subdirs] [/install] [/reboot]*

ドライバーパッケージをドライバーストアに追加します。  
```
/subdirs - traverse sub directories for driver packages.  
/install - install/update drivers on any matching devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/delete-driver** *< oem # .inf > [/uninstall] [/force] [/reboot]*

ドライバーストアからドライバーパッケージを削除します。  

```
/uninstall - uninstall driver package from any devices using it.  
/force - delete driver package even when it is in use by devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/export-driver** <em>< oem # .inf |* > <target directory></em>

ドライバーパッケージをドライバーストアからターゲットディレクトリにエクスポートします。

**/enumdrivers**

ドライバーストア内のすべてのサードパーティ製ドライバーパッケージを列挙します。

**/disabledevice** <em>\<インスタンス ID\> [/reboot]</em>

**Windows 10 バージョン2004以降でのみ使用可能**

システム上のデバイスを無効にします。 

```
/reboot - reboot system if needed to complete the operation.
```

**/enabledevice** *\<インスタンス ID\> [/reboot]*

**Windows 10 バージョン2004以降でのみ使用可能**

システム上のデバイスを有効にします。  

```
/reboot - reboot system if needed to complete the operation.
```

**/restart-device** *\<インスタンス ID\> [/reboot]*

**Windows 10 バージョン2004以降でのみ使用可能**

システム上のデバイスデバイスを再起動します。 

```
/reboot - reboot system if needed to complete the operation.
```

**/remove-device** *\<インスタンス ID\> [/サブツリー] [/reboot]*

**Windows 10 バージョン2004以降でのみ使用可能**

システムからデバイスを削除しようとしています。 

```
/subtree - remove entire device subree, including any child devices.
/reboot - reboot system if needed to complete the operation.
```

**/scan-devices** *[/INSTANCEID \<インスタンス ID\>] [/async]*

**Windows 10 バージョン2004以降でのみ使用可能**

システムをスキャンして、デバイスのハードウェアの変更を確認します。 

```
/instanceid <instance ID> - scan device subtree for changes.
/async - scan for changes asynchronously.
```
**/接続デバイス** *[/接続] [/切断] [/INSTANCEID \<インスタンス ID\>] [/クラス < 名前 |GUID >] [/問題 [\<問題コード\>]] [/id] [/関係] [/ドライバー]*

**Windows 10 バージョン1903以降でのみ使用可能**

システム上のすべてのデバイスを列挙します。

```
/connected | /disconnected - filter by connected devices or filter by disconnected devices.
/instanceid <instance ID> - filter by device instance ID.
/class <name | GUID> - filter by device class name or GUID.
/problem [<code>] - filter by devices with problems or filter by specific problem code.
/ids - display hardware IDs and compatible IDs.
/relations - display parent and child device relations.
/drivers - display matching and installed drivers.
```

**/enumインターフェイス** *[/有効 |/無効] [/クラス \<GUID\>]*

**Windows 10 バージョン1903以降でのみ使用可能**

システム上のすべてのデバイスインターフェイスを列挙します。

```
/enabled | /disabled - filter by enabled interfaces or filter by disabled interfaces.
/class <GUID> - filter by interface class GUID.
```

**/?**

コマンドライン構文を表示します。

## <a name="legacy-command-mapping"></a>レガシコマンドマッピング

次のコマンドは引き続きサポートされていますが、従来のコマンドです。  代わりに、最新の構文を使用することをお勧めします。

```
  -a [-i]  <filename.inf> ==> /add-driver <filename.inf> [/install]

  -d [-f]  <oem#.inf>     ==> /delete-driver <oem#.inf> [/force]

  -e                     ==> /enum-drivers
```
 

###  <a name="comments"></a>コメント



PnPUtil ツールの使用方法の例については、「 [pnputil の例](pnputil-examples.md)」を参照してください。

 

 





