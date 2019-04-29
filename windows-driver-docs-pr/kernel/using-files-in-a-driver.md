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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387401"
---
# <a name="using-files-in-a-driver"></a>ドライバーでのファイルの使用





Microsoft Windows 役員でファイルを表します*ファイル オブジェクト*、これらは、オブジェクト マネージャーで管理されている executive オブジェクトです。 (ディレクトリもオブジェクトによって表されますファイルです。)

カーネル モードのコンポーネントが、これはオブジェクト名、ファイルを参照して **\\\dosdevices\z**ファイルの完全なパスを連結します。 (Microsoft Windows 2000 と以降のバージョン、オペレーティング システムの**\\いますか。** 等価 **\\\dosdevices\z**)。たとえば、オブジェクト名を c: の\\WINDOWS\\example.txt ファイルが **\\\dosdevices\z\\c:\\WINDOWS\\example.txt**します。 オブジェクト名を使用して、ファイルを識別するハンドルを開きます。 オブジェクト名の詳細については、次を参照してください。[オブジェクト名](object-names.md)します。

### <a name="to-use-a-file"></a>ファイルを使用するには

1.  ファイルを識別するハンドルを開きます。

    詳細については、次を参照してください。[ファイル ハンドルを開く](opening-a-handle-to-a-file.md)します。

2.  適切な呼び出し、目的の操作を実行**Zw*Xxx*ファイル**ルーチン。

    詳細については、次を参照してください。[ファイル ハンドルを使用して](using-a-file-handle.md)します。

3.  呼び出すことで、ハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。

ファイルを識別するハンドルを開くたびには、Windows 役員が、ファイルを表すファイル オブジェクトを作成し、そのオブジェクトへの開いているハンドルを返します。 そのため、複数のファイル オブジェクトは、1 つのファイルに対して存在できます。 (ユーザー モード アプリケーションがハンドルをコピーできますので、複数のハンドルできますも存在ファイルと同じオブジェクトで)。ファイル オブジェクトへのすべての開いているハンドルが閉じられた後、Windows の役員は、ファイル オブジェクトを削除します。

 

 




