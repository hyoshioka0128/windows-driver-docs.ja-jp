---
title: 45 の例を追加およびドライバー パッケージの削除
description: 45 の例を追加およびドライバー パッケージの削除
ms.assetid: 36da02d7-0b8f-40ed-a594-0e2374595782
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8342c4db377eb4c8c0153800336349a5e514ebb6
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349171"
---
# <a name="example-45-add-and-remove-driver-packages"></a>例 45: ドライバー パッケージを追加および削除する


次の例では、DevCon を使用して、追加、削除、およびドライバー ストアにサード パーティ (OEM) のドライバー パッケージを表示する方法を示します。

最初のコマンドを[ **DevCon Dp\_追加**](devcon-dp-add.md)コマンド、トースター ドライバー ストアに WDK サンプル ドライバーのコピー、INF ファイルは、%windir%\\inf ディレクトリ。 コマンドには、トースター サンプル ドライバーの INF ファイルへの完全修飾パスが含まれています。

このコマンドは、サード パーティ (OEM) ドライバーとデバイスのものですが、トースター サンプルを使用してコマンドをテストすることができます。

```
devcon dp_add C:\WinDDK\5322\src\general\toaster\inf\i386\toaster.inf
```

応答では、DevCon は、ドライバー ストアにトースター INF ファイルを追加し、Oem2.inf ということを報告します。

```
Driver Package 'oem2.inf' added.
```

ドライバー ストアにコピーすることは、前に、Windows は、重複するファイルを追加しているしないことを確認するドライバー ストア内の INF ファイルのバイナリのバージョンに INF ファイルのバイナリ バージョンを比較します。 たとえば場合 Toaster.inf をドライバー ストアに追加するコマンドを繰り返すと、DevCon は作成されません新しい OEM\*.inf ファイル。 だけ、DevCon 出力を次に示すように、既存のファイルの名前を報告します。

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.

devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
Driver Package 'oem2.inf' added.
```

トースター ドライバーのドライバー パッケージをドライバー ストアから削除するには、OEM を使用する必要があります\*ドライバーの .inf ファイル名。 ドライバーのファイル名を検索するには、使用、 [ **DevCon Dp\_enum** ](devcon-dp-enum.md)コマンド。

次のコマンドは、すべての OEM ドライバー パッケージとそのプロパティのいくつかを示します。

```
devcon dp_enum
```

応答では、DevCon には、次の表示が生成されます。

```
c:\WinDDK\5322\tools\devcon\i386>devcon dp_enum
The following 3rd party Driver Packages are on this machine:
oem2.inf
    Provider: Microsoft
    Class: unknown
    Date: 12/10/2004
    Version: 2.0.1403.0
```

この情報は、指定されていないデバイス クラス (トースター) を使用して、Microsoft によって提供されるドライバー パッケージは OEM2.inf、ということを示します。 この情報を使用して、ファイルに関連付けられているドライバー パッケージを削除することができます。

次のコマンドは、その関連付けられているプリコンパイル済み INF (.pnf)、カタログ (.cat) ファイルと共に、ドライバー ストアから OEM2.inf ファイルを削除します。 コマンドは、OEM\*.inf ファイル名。

```
devcon dp_delete oem2.inf
```

応答では、DevCon には、コマンドが成功を示すメッセージが表示されます。

```
Driver Package 'oem2.inf' deleted.
```

OEM\*の .inf ファイル名が必要な[ **DevCon Dp\_削除**](devcon-dp-delete.md)コマンド。 INF ファイルの元の名前を使用しようとする場合、コマンドは失敗、DevCon 出力を次に示すようにします。

```
devcon dp_delete C:\WinDDK\5322\src\general\toa
ster.inf
Deleting the specified Driver Package from the machine failed.
devcon failed.
```

 

 





