---
title: PnPUtil コマンドの構文
description: 構文とパラメーターを含む、pnputil ツールを実行する方法。
ms.assetid: f14ceb98-8d82-43dd-b06e-2595b59b6999
keywords:
- PnPUtil コマンドの構文のドライバーの開発ツール
topic_type:
- apiref
api_name:
- PnPUtil
api_type:
- NA
ms.date: 01/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: b591b0ab1676b56e5b35db7c7cc9c1bb77ed7f89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536828"
---
# <a name="pnputil-command-syntax"></a>PnPUtil コマンドの構文


Pnputil ツールを実行するには、コマンド プロンプト ウィンドウを開き (**管理者として実行**) し、次の構文とパラメーターを使用してコマンドを入力します。

**注**  PnPUtil (PnPUtil.exe) は、Windows、Windows Vista 以降のすべてのバージョンに含まれる (%windir% で\\system32 ディレクトリ)。

 

```
pnputil [/add-driver <...> | /delete-driver <...> |
         /export-driver <...> | /enum-drivers | /?]
```

## <a name="commands"></a>コマンド

  **/add-driver** <filename.inf | *.inf> [/subdirs] [/install] [/reboot]

ドライバー パッケージをドライバー ストアに追加します。  
```
/subdirs - traverse sub directories for driver packages.  
/install - install/update drivers on any matching devices.  
/reboot - reboot system if needed to complete the operation.  
```

  **/delete-driver** *<oem#.inf> [/uninstall] [/force] [/reboot]*

ドライバー ストアからドライバー パッケージを削除します。  

```
/uninstall - uninstall driver package from any devices using it.  
/force - delete driver package even when it is in use by devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/export-driver** <em><oem#.inf | *> <target directory></em>

ターゲット ディレクトリにドライバー ストアからドライバー パッケージをエクスポートします。

**/enum-drivers**

すべてのサード パーティ ドライバー パッケージをドライバー ストアを列挙します。

**/?**

コマンドラインの構文を表示します。

## <a name="legacy-command-mapping"></a>レガシ コマンドのマッピング

次のコマンドはまだサポートされているがレガシ。  最新の状態の構文を使用することをお勧めします。

```
  -a [-i]  <filename.inf> ==> /add-driver <filename.inf> [/install]

  -d [-f]  <oem#.inf>     ==> /delete-driver <oem#.inf> [/force]

  -e                     ==> /enum-drivers
```
 

###  <a name="comments"></a>コメント



PnPUtil ツールを使用する方法の例については、[PnPUtil 例](pnputil-examples.md)を参照してください。

 

 





