---
title: COM ポート データベース
description: COM ポート データベース
ms.assetid: c9baf147-6e33-4ed2-b682-c141938eb0da
keywords:
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
- COM ポート データベース WDK シリアル デバイス
- COM ポート番号の WDK シリアル デバイス
- ポート番号の WDK シリアル デバイス
- ポート番号を解放します。
- 現在のポート番号使用状況 WDK シリアル デバイス
- WDK の COM ポート データベースのサイズ
- COM ポートのデータベースのサイズ変更
- WDK の COM ポートのデータベースのデータベース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed3a09f0d0b8450c87283006f0c79d0c9ea46d36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345050"
---
# <a name="com-port-database"></a>COM ポート データベース

COM ポートのシステムが指定したデータベースが別の COM ポート番号の使用を介し[COM ポート](configuration-of-com-ports.md)システムにインストールされています。 Microsoft Windows は、このコンポーネントを提供します。 ポート COM のインストールを容易にすると、具体的には、各ポート番号を確実に割り当てられている、最大で 1 つのポート。 コンポーネントは、データベースのインストール ソフトウェアがデータベースにアクセスするために呼び出す関数が含まれるライブラリで構成されます。 COM ポートのすべてのシステムが指定したインストーラーでは、COM ポートのデータベースを使用して、COM ポートの番号を取得します。 プラグ アンド プレイ要件ではありませんが、すべてのベンダーから提供されたインストーラーが COM ポートの番号を取得するのに COM ポート データベースを使用する必要がありますも。

COM ポートのデータベースをサポートするルーチンの詳細については、com ポートのデータベース サポート ルーチンを参照してください。

[ComDBClaimNextFreePort](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbclaimnextfreeport)
[ComDBClaimPort](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbclaimport)
[ComDBClose](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbclose)
[ComDBGetCurrentPortUsage](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbgetcurrentportusage)
 [ComDBOpen](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbopen)
[ComDBReleasePort](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbreleaseport)
[ComDBResizeDatabase](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-comdbresizedatabase)

また、次のルーチンを参照してください。

[SerialDisplayAdvancedSettings](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-serialdisplayadvancedsettings)、COM ポートを高度なプロパティ ページをインストールするためのシステム指定のルーチンは[PPORT_ADVANCED_DIALOG](https://msdn.microsoft.com/library/windows/hardware/ff546956(v=vs.85).aspx)-ベンダーから提供されたオプションを提供するルーチン、型指定されました。ダイアログ ボックスによって呼び出される**SerialDisplayAdvancedSettings**

インストーラーでこれらのルーチンを呼び出すリンクをインストーラー *msports.lib*、Windows Driver Kit (WDK) で指定されます。

## <a name="structure-of-the-com-port-database"></a>COM ポートのデータベースの構造

COM ポートのデータベースは、COM ポート番号は、使用するかどうかを示す各要素の配列で構成されます。 配列の最初の要素 COM1、COM2 というように、2 つ目が対応します。 ただし、データベースでは、について、指定したポート番号がこのデバイスに割り当てられているすべての情報は含まれません。 データベースのサイズでは、データベースが現在調停ポート番号の数と同じです。 データベースを介しポート番号の最小数は COMDB\_MIN\_ポート\_調停と調停が最大数は COMDB\_最大\_ポート\_調停です。 使用して、データベースのサイズを増やすことが、 [ **ComDBResizeDatabase** ](https://msdn.microsoft.com/library/windows/hardware/ff546480)ルーチン。

## <a name="opening-and-closing-the-com-port-database"></a>COM ポートのデータベースの開閉

COM ポートのデータベースを使用する前に、クライアントは、呼び出すことによって、データベースを開く必要があります、 [ **ComDBOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff546476)ルーチンをデータベースを識別するハンドルを取得します。 データベースは、任意の連続したデータベースのアクセス中に相互排除によって保護されます。 ただし、データベースを排他的に使用、開くことができませんおよびデータベースへの個別のアクセスとの間の状態を動的に変更できます。

## <a name="determining-the-current-usage-of-com-port-numbers"></a>COM ポート番号の現在の使用量を決定します。

COM ポート番号が既に使用して呼び出すことによって、COM ポートのデータベースを開いた後、クライアントが決定できます、 [ **ComDBGetCurrentPortUsage** ](https://msdn.microsoft.com/library/windows/hardware/ff546474)ルーチン。

通常、クライアントは、次のタスクを実行します。

1. データベースに現在調停されているポート番号の数を決定するルーチンを呼び出します。

2. 各ビットやバイトを対応するポート番号は、使用するかどうかを指定する場所をビットの呼び出し元が割り当てた配列またはバイト配列でポート番号の使用状況に関する情報を返すルーチンを 2 回目を呼び出します。

データベース内のすべてのポート番号が使用、または現在使用可能な適切なポート番号がない、データベースがクライアントにサイズを変更できます。 詳細については、COM ポートのデータベースのサイズ変更を参照してください。

## <a name="obtaining-and-releasing-a-com-port-number"></a>取得および COM ポート番号を解放します。

クライアントは、次のルーチンのいずれかを呼び出すことによって COM ポート番号を取得できます。

- [**ComDBClaimNextFreePort**](https://msdn.microsoft.com/library/windows/hardware/ff546469)、最小の使用可能なポート番号を要求します。

- [**ComDBClaimPort**](https://msdn.microsoft.com/library/windows/hardware/ff546472)、特定のポート番号を要求しようと試みます。

C*laiming* COM ポートのデータベース内の COM ポート番号が「使用中」としてポート番号を記録します。

クライアントが呼び出すことでポート番号を解放、 [ **ComDBReleasePort** ](https://msdn.microsoft.com/library/windows/hardware/ff546477)ルーチン。

## <a name="resizing-the-com-port-database"></a>COM ポートのデータベースのサイズ変更

サイズと、クライアントが呼び出すことによって、COM ポートのデータベースを変更、 [ **ComDBResizeDatabase** ](https://msdn.microsoft.com/library/windows/hardware/ff546480)ルーチン。 クライアントは、整数では、データベースのサイズが 1024 の倍数を増やすだけことができます。 データベースの最大サイズは COMDB\_最大\_ポート\_調停です。
