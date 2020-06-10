---
title: キュー固有ファイルのダウンロード
description: キュー固有ファイルのダウンロード
ms.assetid: b6aad46a-2934-461a-ad11-6ad699687fc1
keywords:
- キュー固有のプリンターファイルをダウンロードしています
- WDK、キュー固有のファイルをポイントして印刷する
- キュー固有ファイル WDK プリンター
- 印刷キューの WDK、ポイント、および印刷
- WDK プリンター、ポイント、および印刷をキューに置いています
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1ccd7e3e80919bc9d0ee467c89e18f7d80c507b4
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638438"
---
# <a name="downloading-queue-specific-files"></a>キュー固有ファイルのダウンロード

ユーザーがクライアントシステムからプリントサーバーへのプリンター接続を作成することにした場合、インストールアプリケーションで、「[プリンターのインストール中にサポートポイントと印刷](supporting-point-and-print-during-printer-installations.md)」で説明されているレジストリエントリを作成した場合、次のイベントが発生します。

1. ユーザーアプリケーションは**Addprinterconnection**接続を呼び出します。これについては、Microsoft Windows SDK のドキュメントを参照してください。

1. クライアントのリモート印刷プロバイダー (Win32spl.dll) は、サーバーへの接続を作成します。

1. サーバーのスプーラでは、ドライバーファイルがクライアントに送信されます。

1. クライアントの Win32spl.dll は、サーバー上で enumprinter Key および enumprinter Dataex を呼び出して、プリンターのレジストリエントリをコピーします。

1. サーバーのスプーラが Enumprinter Dataex の処理中にレジストリ値を列挙すると、次の操作が実行されます。これは、 **copyfiles \\ ICM**など、プリンターの**copyfiles**キーのサブキーが検出されるたびに実行されます。

    - 指定されている場合は[ポイントアンドプリント DLL](point-and-print-dlls.md)を読み込み、 [**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)関数を呼び出します。これにより、ソースパスまたはターゲットパスを変更できます。

    - **GenerateCopyFilePaths**によって返されたソースとターゲットのパスに基づいて**SourceDir**キーと**TargetDir**キーを作成し、それらを enumプリンター dataex データとしてクライアントスプーラに返します。 (これらのキーはサーバーに実際には存在しません)。

1. クライアントの Win32spl.dll は、enumprinter Data および enumprinter Dataex 呼び出しへの応答として受信したプリンターキーをキャッシュします。

1. **Copyfiles \\ ICM**など、プリンターの**copyfiles**キーの各サブキーについて、クライアントの win32spl.dll は次の操作を実行します。

    - ローカルポイントと印刷 DLL が提供されている場合は、それを読み込み、その**GenerateCopyFilePaths**関数を呼び出します。これにより、ソースパスと宛先パスを変更できます。 (入力は、サーバーから受信した**SourceDir**キーと**TargetDir**キーです)。

    - **ファイル**キーに関連付けられているすべてのファイルをサーバーからダウンロードします。

    - ポイントと印刷ファイルがダウンロードされたことを示すイベントをログに記録します。

    - DLL が提供されている場合、ポイントアンドプリント DLL の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出し、COPYFILE \_ イベントファイルの変更イベントを指定し \_ \_ ます。

1. クライアントスプーラは、プリンタ[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ イベントキャッシュ更新イベントを指定して、ドライバの DrvPrinterEvent 関数を呼び出し \_ \_ ます。

1. クライアントスプーラは、プリンタイベントの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ ADD CONNECTION イベントを指定して、ドライバの DrvPrinterEvent 関数を再度呼び出し \_ \_ ます。

1. ポイントアンドプリント DLL が指定されている場合、クライアントスプーラは[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出し、COPYFILE \_ イベントの \_ プリンタ接続の追加イベントを指定し \_ \_ ます。

## <a name="connection-example"></a>接続の例

例として、インストールアプリケーションで、インストールの例で説明されているサーバーレジストリエントリが定義されているとします。 また、サーバーに NTPRINT.INF という名前を付け、クライアントに MyClient という名前を付けているとします。

NTPRINT.INF で、HpColor という名前の印刷キューに接続するために、MyClient のユーザーアプリケーションは次のように**Addprinterconnection**接続を呼び出します。

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

サーバーでは、スプーラは Mscms を読み込み、次のように[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)を呼び出します。

```cpp
GenerateCopyFilePaths(
    "HpColor",
    "Color",
    &SplclientInfo1,
    1,
    \\NTPRINT\PRINT$\Color,
    &dwSourceDirSize,
    "Color",
    &dwDestDirSize,
    COPYFILE_FLAG_SERVER_SPOOLER)
```

Microsoft ICM の Mscms モジュールは、ソースまたはターゲットのパスを変更しないため、エラーの成功だけを返し \_ ます。

サーバースプーラは、MyClient に次のキーを返します。

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

クライアントでは、 **TargetDir**の値は C: \\ Winnt System32 Spool ドライバーの色に展開され \\ \\ \\ \\ ます。

MyClient のスプーラは、次の操作を実行します。

- Mscms をダウンロードし、次のように[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)を呼び出します。

    ```cpp
    GenerateCopyFilePaths(
        "\\NTPRINT\HpColor",
        "Color",
        &SplclientInfo1,
        1,
        \\NTPRINT\PRINT$\Color,
        &dwSourceDirSize,
        "C:\Winnt\System32\Spool\Drivers\Color",
        &dwDestDirSize,
        COPYFILE_FLAG_CLIENT_SPOOLER)
    ```

    Microsoft ICM の Mscms モジュールは、ソースまたはターゲットのパスを変更しないため、エラーの成功だけを返し \_ ます。

- Hpclrlsr. icm を C: \\ Winnt \\ System32 \\ Spool ドライバーの \\ \\ 色にダウンロードします。

- ポイントと印刷ファイルがダウンロードされたことを示すイベントをログに記録します。

- COPYFILE [**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) \_ イベントファイル CHANGED イベントを指定して、Mscms 内の SpoolerCopyFileEvent 関数を呼び出し \_ \_ ます。

- プリンター [**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ イベントキャッシュ更新イベントを指定して、プリンタードライバーの DrvPrinterEvent 関数を呼び出し \_ \_ ます。

- プリンター [**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ イベント ADD CONNECTION イベントを指定して、プリンタードライバーの DrvPrinterEvent 関数を再度呼び出し \_ \_ ます。

- Mscms 内の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出します。このとき、COPYFILE イベントの [プリンター接続の追加] イベントを指定し \_ \_ \_ \_ ます。
