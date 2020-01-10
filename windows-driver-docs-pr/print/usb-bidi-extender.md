---
title: USB 双方向エクステンダー
description: Bidi XML ファイルと、USB Bidi エクステンダーと呼ばれる Javascript ファイルの組み合わせを使用した、USB デバイスの Bidi サポートについて説明します。
ms.assetid: C4012369-F1C6-4EBC-8DAE-F4E551DE782D
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: cf0b03ad984b6c99f0006be1b8ac929a9f063a63
ms.sourcegitcommit: 3fbf71b2bd92abca0bfb3c373f57af9a0eb67c93
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75775726"
---
# <a name="usb-bidi-extender"></a>USB 双方向エクステンダー

Windows では、製造元は、Bidi XML ファイルと、USB Bidi エクステンダーと呼ばれる Javascript ファイルの組み合わせを使用して、USB デバイスの双方向通信 (Bidi) をサポートできます。

USB Bidi エクステンダーを使用すると、アプリケーションは、トランスポートメカニズムとして、USB で Bidi を使用できます。 Javascript の実装では、デバイスフロー制御はサポートされていません。また、印刷中に印刷ジョブを使用するコントロール情報の多重化もサポートされていません。

既定では、Bidi クエリとステータス要求は、印刷に使用される USB デバイスインターフェイスを介してルーティングされます。 これにより、 **getschemas** javascript メソッドを使用して状態の完全な双方向通信を行うことができます。また、 **setschema** javascript メソッドを使用して Set 操作を許可することもできます。 印刷デバイスに送信される印刷ジョブがない場合でも、完全な双方向通信が可能です。

印刷中、書き込みは印刷ジョブデータによってブロックされるため、 **getStatus**メソッドを使用して、読み取りチャネルのみを使用して、デバイスから要求されていない状態を取得します。 ただし、デバイスでセカンダリ USB インターフェイスがサポートされている場合は、 **Requeststatus**メソッド関数を使用して、デバイスの印刷中にプリンターから状態を取得します。

Windows 8.1 には、ホストベースのデバイスをサポートするために v4 ドライバーモデルが拡張されています。 さらに、USBMon は、Ihv が JavaScript コードを使用して、印刷パスをより適切に制御し、印刷ジョブベースのアクションを実行できるように更新されました。 この更新プログラムには、新しい Bidi JavaScript エントリポイントを提供する Api が追加されています。 これらの Api は、USBMon の既存の関数に合わせて調整されます。

**startPrintJob**。 この新しい関数は、USBMon の startDocPort と整合しています。 ホストベースの印刷デバイスに接続されているポートで新しい USB 印刷ジョブが開始されるたびに、USBMon は IHV 提供の JavaScript を呼び出して、必要なジョブ処理の実行を許可します。 これには、ジョブのグローバルプロパティをジョブプロパティバッグに設定し、デバイスに現在の状態と構成データのクエリを実行したり、何も行わないようにしたりすることができます。 完了したタスクは、デバイスと IHV に完全に依存しています。

**Writeprintdata**。 この新しい関数は、USBMon の writePort と整合しています。 USBMon が印刷処理中にスプーラから各 writePort 関数呼び出しを受け取ると、指定された印刷データを IHV JavaScript 関数を介してホストベースのデバイスに送信する必要があります。 これにより、IHV JS は、この時点でデバイスに送信されるものを決定できます。 IHV は、必要に応じて、データバッファーの一部を削除、追加、または保存できます。 これにより、IHV は、のときにデバイスに送信される内容を完全に制御できます。 これにより、すべてのデータがスプーラから受信された後に処理する印刷ジョブの偶数ページに対して、(永続ストリームのいずれかの) データを保存する機会を IHV に与えることで、このようなシナリオを手動で双方向にすることができます。 また、IHV は、printerBidiSchemaResponses オブジェクトを使用して、ジョブの処理中に印刷ジョブの状態またはデバイスの状態を返すこともできます。

**endPrintJob**。 この新しい関数は、USBMon の endDocPort と整合しています。 USBMon は、ホストベースの印刷デバイスに接続されているポートで各 USB 印刷ジョブの endDocPort 呼び出しを受信するときに、必要な処理後の処理を可能にするために、IHV 提供の JavaScript を呼び出します。 これには、保持されているデータをデバイスに送信することが含まれる場合があります。これには、手動の二重を開始するための Bidi スキーマ値、または IHV/デバイスが必要とするその他のものが

次の図は、USB Bidi 拡張アーキテクチャの概要を示しています。このシナリオでは、 **getStatus**メソッドを使用して、usbprint インターフェイスを介してデバイスから要求されていないステータスを取得します。

![getstatus メソッドを使用した usb bidi エクステンダーアーキテクチャ](images/usbbidiext-arch.png)

USB プリンターの操作の詳細については、「 [Usb 印刷](usb-printing.md)」を参照してください。

## <a name="usb-bidi-extender-api-reference"></a>USB Bidi extender API リファレンス

USB Bidi extender の JavaScript コードは、次の機能を使用して、印刷デバイスと通信します。

- **getSchemas**

- **setSchema**

- **getStatus**

- **requestStatus**

- **startPrintJob**

- **writePrintData**

- **endPrintJob**

これらの Api の詳細については、「 [JAVASCRIPT Api Reference](javascript-api-reference-.md)」を参照してください。

## <a name="usbmon-bidi-extension-xml-schema"></a>USBMon Bidi 拡張 XML スキーマ

USBMon Bidi 拡張ファイルは、SNMP Bidi 拡張ファイルと WSDMon Bidi 拡張ファイルと同じ基本的な構造を使用します。 XML スキーマファイルは Windows Driver Kit に発行され、USBMon Bidi 拡張ファイルは INFGate のテスト中に自動的にスキーマ検証されます。 Bidi 拡張スキーマを開発し、USB バスを操作するときは、次の情報に注意することが重要です。

- 値には、Get、Set、または GetSet の accessType を指定できます。 これは、記述されたスキーマ要素が、Bidi の Get または Set 操作の種類でサポートされる場所を示します。

- 値には queryKey を指定できます。 これは、デバイスからデータを取得するために使用される物理操作を示すために使用する必要があります。 [印刷ドライバーの usb モニターと Bidi サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)は、2つの異なる querykeys をサポートする usb デバイスを示しています。 同じ queryKey の下にあるすべてのプロパティは、1つの USB 読み取り/書き込み操作で取得可能である必要があります。

- Bidi 値は、Bidi API 呼び出しで要求された場合、すぐにポーリングされます。 RefreshInterval 値は、特定の Bidi スキーマ値の更新プログラムをデバイスにポーリングするタイミングを示す初期値です。 ポーリングが行われるたびに、ポーリングが停止するまで refreshInterval が増加します。 次の数式は、refreshInterval のインクリメント方法を示しています。

    ```javascript
    currentRefreshInterval = refreshInterval * (3 * numPolls);
    ```

## <a name="usbmon-and-usb-bidi-extension-file-interaction"></a>USBMon および USB Bidi 拡張ファイルの相互作用

新しい USB ポートが作成または開かれるたびに、USBMon によって、接続されているデバイスと関連するドライバーに新しい Bidi 拡張ファイルと Bidi 拡張機能 JavaScriptfile が含まれているかどうかが判断されます。 USBMon は、v4 ドライバーマニフェストまたはドライバー INI ファイルを検索し、ファイルの名前を取得します。 USBMon が関連するファイルを検出すると、それらを使用して、このデバイスでサポートされている拡張 Bidi スキーマ値の一覧を特定し、デバイスと通信してそのファイルの値を照会します。 この時点で、USBMon は、既存の印刷スプーラ Api を介して、IHV が指定した Bidi スキーマアクションをサポートしています。

## <a name="windows-driver-samples-on-github"></a>GitHub の Windows ドライバーのサンプル

**Usbmon BIDI Xml ファイルのサンプル**-Usbmon BIDI 拡張 XML ファイルのサンプルを提供します。 標準の Bidi スキーマプロパティ DeviceInfo、構成、およびメモリを使用し、いくつかのカスタム拡張機能も定義します。 詳細については、「[印刷ドライバーの USB モニター」および「Bidi サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)」を参照してください。

Bidi 拡張ファイルの詳細については、「[双方向通信スキーマ](bidirectional-communication-schema.md)」を参照してください。

**Usbmon Bidi JavaScript ファイルのサンプル**です。 このサンプルには、USBMon Bidi Extender JavaScript ファイルが含まれています。 これは、Bidi の SET 操作と GET 操作をサポートする方法、およびプリンターの印刷中にイベントをリッスンする方法を示しています。 詳細については、「[印刷ドライバーの USB モニター」および「Bidi サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)」を参照してください。

デバッグ

次のレジストリキーを作成して、対話型デバッグを有効にすることができます。 USB Bidi JavaScript では、デバッグを有効にする前に、印刷スプーラを再起動する必要があります。

**キー名:** HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷

**値の名前:** EnableJavaScriptDebugging

**型:** DWORD

**値:** 1

前のセクションで示したレジストリキーが作成され、ホストプロセスが再起動されると、スクリプトは次のようにデバッグできます。

1. ホストプロセスにデバッガーをアタッチします。 USB Bidi JavaScript の場合、これは spoolsv.exe です。

2. デバッガーをスクリプトデバッグモードに設定します。

3. **[すべて中断]** (Ctrl + Alt + Break) を選択すると、スクリプトの次回実行時にプロセスが中断されます。

4. シナリオを実行して問題を再現します。

5. デバッガーが JavaScript 関数に分割されたら、必要なブレークポイントを設定し、コードをステップ実行します。

## <a name="related-topics"></a>関連トピック

[双方向通信スキーマ](bidirectional-communication-schema.md)  

[IPrinterBidiSchemaElement](iprinterbidischemaelement-interface.md)  

[IPrinterScriptContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  

[JavaScript API リファレンス](javascript-api-reference-.md)  

[印刷ドライバーの USB モニターと Bidi サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)  

[USB 印刷](usb-printing.md)  

[V4 プリンタードライバーの接続](v4-printer-driver-connectivity.md)
