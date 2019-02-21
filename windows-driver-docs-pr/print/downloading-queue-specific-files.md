---
title: キューに固有のファイルのダウンロード
description: キューに固有のファイルのダウンロード
ms.assetid: b6aad46a-2934-461a-ad11-6ad699687fc1
keywords:
- プリンターのキューに固有のファイルのダウンロード
- ポイント アンド プリントの WDK、キューに固有のファイル
- WDK のプリンターをキューに固有のファイル
- 印刷キューの WDK、ポイント アンド プリント
- キューの WDK プリンター、ポイント アンド プリント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96e29981841ccda93d675da69bec12d6b077517
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527510"
---
# <a name="downloading-queue-specific-files"></a>キューに固有のファイルのダウンロード





ユーザーが自分のクライアント システムからプリント サーバー、プリンターの接続を作成し、インストール アプリケーションで説明されているレジストリ エントリを作成した場合[サポート ポイントとプリンターのインストール中に印刷](supporting-point-and-print-during-printer-installations.md)で、次のイベントが発生します。

1.  ユーザーのアプリケーション呼び出し**AddPrinterConnection**、これは、Microsoft Windows SDK ドキュメントで説明します。

2.  クライアントのリモート印刷プロバイダー (Win32spl.dll) では、サーバーへの接続を作成します。

3.  サーバーのスプーラは、ドライバー ファイルをクライアントに送信します。

4.  クライアントの Win32spl.dll は、プリンターのレジストリ エントリのコピー先サーバーで EnumPrinterKey と EnumPrinterDataEx を呼び出します。

5.  プリンターのサブキーが出現するたび、次の操作を実行、サーバーのスプーラ EnumPrinterDataEx の処理中にレジストリ値を列挙、 **CopyFiles**キーなど、 **CopyFiles\\ICM**:
    -   読み込み、[ポイントと印刷 DLL](point-and-print-dlls.md)指定するを呼び出している場合、その[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896)関数で、ソースまたは変換先のパスを変更することができます。
    -   作成**SourceDir**と**TargetDir**から返される元とコピー先のパスに基づくキー **GenerateCopyFilePaths**、として、クライアントのスプーラーに返しますEnumPrinterDataEx データ。 (これらのキー実際に存在しないサーバーにします。)

6.  クライアントの Win32spl.dll EnumPrinterData への応答で受信したプリンターのキーをキャッシュし、EnumPrinterDataEx を呼び出します。

7.  プリンターの各サブキーの**CopyFiles**キーなど、 **CopyFiles\\ICM**クライアントの Win32spl.dll は、次の操作を実行します。
    -   提供される、1 つを呼び出す場合、ローカルのポイントと印刷の DLL を読み込み、 **GenerateCopyFilePaths**関数で、ソースまたは変換先のパスを変更することができます。 (入力値は、 **SourceDir**と**TargetDir**キーがサーバーから受信します)。
    -   関連付けられているすべてのファイルをダウンロード、**ファイル**サーバーからキー。
    -   ポイント アンド プリントのファイルがダウンロードされたことを示す、イベント ログに記録します。
    -   ポイントと印刷の DLL を呼び出す[ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681)関数は、DLL を指定すると、COPYFILE を指定する場合\_イベント\_ファイル\_CHANGED イベント。

8.  クライアントのスプーラー呼び出してドライバーの[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)関数、プリンターを指定する\_イベント\_キャッシュ\_更新イベント。

9.  クライアントのスプーラー呼び出してドライバーの[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)プリンターを指定する関数を再度、\_イベント\_追加\_接続イベント。

10. クライアントのスプーラーを呼び出す場合は、ポイントと印刷 DLL を指定すると、その[ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681) 、COPYFILE を指定する、関数\_イベント\_追加\_プリンター\_接続イベント。

### <a name="connection-example"></a>接続の例

たとえば、インストール アプリケーションのインストールの例で説明されているサーバーのレジストリ エントリが定義されていると仮定します。 さらに、NTPRINT という名前のサーバーは、クライアントは MyClient という名前を前提としています。

NTPRINT、MyClient 呼び出しでユーザーのアプリケーションで HpColor をという名前の印刷キューへの接続に**AddPrinterConnection**次のようにします。

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

Mscms.dll および呼び出し、サーバーのスプーラを読み込みます[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896)次のようにします。

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

エラーだけを返すように Microsoft ICM の Mscms.dll モジュールが、ソースまたは変換先のパスを変更しません\_成功します。

サーバーのスプーラは、MyClient へ、次のキーを返します。

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

値は、クライアントで**TargetDir** c: 展開\\Winnt\\System32\\スプール\\ドライバー\\色。

MyClient 上のスプーラーは、次の操作を実行します。

-   Mscms.dll と呼び出しダウンロード[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896)次のようにします。

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

    エラーだけを返すように Microsoft ICM の Mscms.dll モジュールが、ソースまたは変換先のパスを変更しません\_成功します。

-   Hpclrlsr.icm を c: ダウンロード\\Winnt\\System32\\スプール\\ドライバー\\色。

-   ポイント アンド プリントのファイルがダウンロードされたことを示す、イベント ログに記録します。

-   呼び出し、 [ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681)関数の指定、COPYFILE Mscms.dll\_イベント\_ファイル\_CHANGED イベント。

-   プリンター ドライバーの呼び出す[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)関数、プリンターを指定する\_イベント\_キャッシュ\_更新イベント。

-   プリンター ドライバーの呼び出す[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)プリンターを指定する関数を再度、\_イベント\_追加\_接続イベント。

-   呼び出し、 [ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681)関数の指定、COPYFILE Mscms.dll\_イベント\_追加\_プリンター\_接続イベント。

 

 




