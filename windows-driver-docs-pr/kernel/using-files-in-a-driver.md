---
title: ドライバーでのファイルの使用
description: ドライバーでのファイルの使用
ms.assetid: 721bf336-1d1d-4677-843d-8af04c6f434d
keywords:
- ファイルの WDK カーネル
- ファイル オブジェクトの WDK カーネル
- WDK のオブジェクトのファイル オブジェクト
- ファイル ハンドルの WDK カーネル
- ファイルの WDK カーネルへのハンドルします。
- ファイルからデータを読み取る
- データ ファイルを書き込む
- ファイルのメタデータの読み取り
- ファイルのメタデータの書き込み
- ドライバー ファイル オブジェクトの WDK カーネル
- 複数のファイル オブジェクトの WDK カーネル
- カーネル モード ドライバー WDK、ファイル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ab1455fd941dce3461e0dea4f8d0ee2ffd5ee0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574354"
---
# <a name="using-files-in-a-driver"></a>ドライバーでのファイルの使用





Microsoft Windows 役員でファイルを表します*ファイル オブジェクト*、これらは、オブジェクト マネージャーで管理されている executive オブジェクトです。 (ディレクトリもオブジェクトによって表されますファイルです。)

カーネル モードのコンポーネントが、これはオブジェクト名、ファイルを参照して **\\\dosdevices\z**ファイルの完全なパスを連結します。 (Microsoft Windows 2000 と以降のバージョン、オペレーティング システムの**\\いますか。** 等価 **\\\dosdevices\z**)。たとえば、オブジェクト名を c: の\\WINDOWS\\example.txt ファイルが **\\\dosdevices\z\\c:\\WINDOWS\\example.txt**します。 オブジェクト名を使用して、ファイルを識別するハンドルを開きます。 オブジェクト名の詳細については、[オブジェクト名](object-names.md)を参照してください。

### <a name="to-use-a-file"></a>ファイルを使用するには

1.  ファイルを識別するハンドルを開きます。

    詳細については、[ファイル ハンドルを開く](opening-a-handle-to-a-file.md)を参照してください。

2.  適切な呼び出し、目的の操作を実行**Zw*Xxx*ファイル**ルーチン。

    詳細については、[ファイル ハンドルを使用して](using-a-file-handle.md)を参照してください。

3.  呼び出すことで、ハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。

ファイルを識別するハンドルを開くたびには、Windows 役員が、ファイルを表すファイル オブジェクトを作成し、そのオブジェクトへの開いているハンドルを返します。 そのため、複数のファイル オブジェクトは、1 つのファイルに対して存在できます。 (ユーザー モード アプリケーションがハンドルをコピーできますので、複数のハンドルできますも存在ファイルと同じオブジェクトで)。ファイル オブジェクトへのすべての開いているハンドルが閉じられた後、Windows の役員は、ファイル オブジェクトを削除します。

 

 




