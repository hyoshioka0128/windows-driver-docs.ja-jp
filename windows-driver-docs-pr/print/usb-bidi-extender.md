---
title: USB 双方向エクステンダー
description: Bidi XML ファイルと USB Bidi エクステンダーと呼ばれる Javascript ファイルの組み合わせを使用して USB デバイスの双方向サポートについて説明します。
ms.assetid: C4012369-F1C6-4EBC-8DAE-F4E551DE782D
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f265d1402c548515773528a57bb419c6dee6059
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578372"
---
# <a name="usb-bidi-extender"></a>USB 双方向エクステンダー


Windows では、双方向の XML ファイルと USB Bidi エクステンダーと呼ばれる Javascript ファイルの組み合わせを使用して、USB デバイスの双方向 (Bidi) の通信をサポートするために製造元をできます。

USB Bidi エクステンダーでは、USB で Bidi をトランスポート メカニズムとして使用するアプリケーションを使用します。 Javascript の実装は、デバイスのフロー制御、または印刷時に印刷ジョブの管理情報の多重化をサポートしていません。

既定、Bidi クエリ、および状態では、要求は、印刷に使用される、USB デバイス インターフェイス経由でルーティングされます。 これにより、完全な双方向通信を使用して状態の**getSchemas** JavaScript メソッドを使用しても、許可の設定操作として、 **setSchema** JavaScript メソッド。 印刷デバイスに送信される印刷ジョブがないときに、完全な双方向の通信が可能です。

印刷ジョブのデータによって、印刷時に書き込みがブロックされているため、 **getStatus**読み取りチャネルのみを使用して、デバイスからの要請されていない状態を取得するメソッドを使用します。 デバイスがセカンダリ USB インターフェイスをサポートしている場合は、 **requestStatus**メソッド関数を使用して、デバイスが印刷中にプリンターの状態を取得します。

Windows 8.1 では、v4 ドライバー モデルがホスト ベースのデバイスのサポートを提供する拡張されました。 さらに、印刷パスの管理性が向上し、印刷ジョブに基づくアクションを実行する JavaScript コードを使用する Ihv を許可する USBMon が更新されました。 更新プログラムには、新しい双方向の JavaScript のエントリ ポイントを提供する Api の追加が含まれています。 これらの Api は、USBMon の既存の機能に揃えて配置されます。

**startPrintJob**します。 この新しい関数は、startDocPort USBMon 内に配置します。 新しい各 USB として印刷ジョブが USBMon 呼び出す必要があります、前のジョブの処理を行うことができる JavaScript が提供されている IHV ホスト ベースの印刷デバイスに接続されているポートで開始されます。 これには、ジョブのプロパティ バッグは、現在の状態と構成データ、または何ものデバイスのクエリでジョブのグローバル プロパティの設定が含まれます。 タスクが完了しましたが、デバイスと IHV に完全に依存します。

**writePrintData**します。 この新しい関数は、writePort USBMon 内に配置します。 USBMon では、印刷の act の中に、スプーラーから各 writePort 関数呼び出しを受信したときに、指定された印刷データを IHV JavaScript 関数を使用して、ホスト ベースのデバイスに送信する必要があります。 これにより、この時点で、デバイスにどのような送信する必要がありますを決定する IHV JS できます。 IHV では、削除、追加、または必要に応じて、データ バッファー内の部分を保存できます。 これにより、デバイスへの送信内容を完全に制御を IHV とき。 これは、IHV に離れた (内で永続的なストリームのいずれか)、スプーラーからすべてのデータを受信した後に処理するための印刷ジョブの偶数ページのデータを保存する機会を提供することにより、手動の二重とは、このようなシナリオを有効にするのに役立ちます。 IHV は printerBidiSchemaResponses オブジェクトを使用しても、ジョブの処理時に印刷ジョブの状態またはデバイスの状態を返します。

**endPrintJob**します。 この新しい関数は、endDocPort USBMon 内に配置します。 USBMon USBMon が行うことができる JavaScript が提供されている IHV を呼び出すホスト ベースの印刷デバイスに接続されているポートで USB 印刷ジョブごとに endDocPort 呼び出しの受信と処理後、ジョブが必要です。 これには、における Bidi スキーマ手差し両面印刷または IHV/デバイスを必要とするその他すべて開始するために値を返す、デバイスに保持されているデータの送信が含まれます。

次の図は、シナリオを示す双方向の USB 拡張機能のアーキテクチャの概要を**getStatus** USBPrint インターフェイスを使用してデバイスからの要請されていない状態を取得するメソッドを使用します。

![getstatus メソッドを使用した usb bidi エクステンダーのアーキテクチャ](images/usbbidiext-arch.png)

USB プリンターの使用方法の詳細については、次を参照してください。 [USB 印刷](usb-printing.md)します。

## <a name="usb-bidi-extender-api-reference"></a>USB Bidi エクステンダー API リファレンス


USB Bidi エクステンダーの JavaScript コードは、印刷デバイスと通信するため、次の関数を使用します。

-   **GetSchemas**

-   **setSchema**

-   **getStatus**

-   **requestStatus**

-   **startPrintJob**

-   **writePrintData**

-   **endPrintJob**

これらの Api の詳細については、次を参照してください。 [JavaScript API リファレンス](javascript-api-reference-.md)します。

## <a name="usbmon-bidi-extension-xml-schema"></a>USBMon 双方向の拡張機能の XML スキーマ


USBMon 双方向の拡張機能ファイルは、SNMP Bidi 拡張ファイルと WSDMon 双方向の拡張機能のファイルとして同じ基本的な構造を使用します。 XML スキーマ ファイルを Windows Driver Kit のパブリッシュであり USBMon 双方向の拡張ファイル自動的にスキーマ検証 INFGate WHCK テスト中にします。 双方向の拡張機能のスキーマを開発すると、USB bus を使用しているは、次の情報に注意してください。

-   値は、Get、セット、または GetSet のいずれかの accessType を指定することができます。 これは、Bidi Get または Set 操作の種類で説明されているスキーマ要素はサポートされていることを示します。

-   QueryKey の値を指定できます。 これは、デバイスからデータを取得するための物理操作を示すために使用する必要があります。 [印刷ドライバー USB モニターおよび Bidi サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)2 つの異なる queryKeys をサポートする USB デバイスを示します。 同じ queryKey 下にあるすべてのプロパティは、1 つの USB 読み取り/書き込み操作で取得できる必要があります。

-   Bidi 値は要求された場合にすぐにポーリングされる Bidi API 呼び出しで。 RefreshInterval 値は、特定の Bidi スキーマ値で更新プログラムのデバイスをポーリングするタイミングを示す初期値です。 ポーリングごとの後までポーリングを停止します、refreshInterval が増加します。 次の数式は、refreshInterval のインクリメント方法を示しています。

    ```javascript
    currentRefreshInterval = refreshInterval * (3 * numPolls);
    ```

## <a name="usbmon-and-usb-bidi-extension-file-interaction"></a>USBMon と USB Bidi 拡張機能ファイルの相互作用


新しい各 USB ポートを作成または開くよう USBMon は接続しているデバイスと、関連するドライバーは、新しい双方向の拡張機能ファイルと双方向の拡張機能 JavaScriptfile かどうかを決定します。 USBMon は v4 ドライバー マニフェストまたはドライバーの INI ファイルを検索し、ファイルの名前を取得します。 USBMon には、関連するファイルが検出されると、このデバイスでサポートされている Bidi スキーマの拡張の値のリストを決定し、その値のクエリを実行するデバイスと通信しに使用します。 この時点で USBMon には、既存の印刷スプーラー Api を介して Bidi スキーマの IHV が指定したアクションがサポートされています。

## <a name="windows-driver-samples-on-github"></a>GitHub の Windows ドライバーのサンプル


**USBMon 双方向の XML ファイルのサンプル**-この USBMon 双方向の拡張 XML ファイルのサンプルを提供します。 Bidi スキーマの標準プロパティ DeviceInfo、構成、およびメモリを使用しても、いくつかのカスタム拡張機能を定義します。 詳細については、次を参照してください。[印刷ドライバー USB モニターおよび Bidi サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)します。

Bibi 拡張ファイルの詳細については、次を参照してください。 および[双方向通信スキーマ](bidirectional-communication-schema.md)します。

**USBMon 双方向の JavaScript ファイルのサンプル**します。 このサンプルには、USBMon 双方向の Extender の JavaScript ファイルが含まれています。 双方向の設定と取得をサポートする方法を示します、操作とプリンターの印刷中にイベントをリッスンする方法。 詳細については、次を参照してください。[印刷ドライバー USB モニターおよび Bidi サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)します。

デバッグ

次のレジストリ キーを作成して対話形式デバッグを有効にすることができます。 USB Bidi の JavaScript デバッグが有効にする前に、印刷スプーラを再起動する必要があります。

**キー名:** HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷

**値の名前:** EnableJavaScriptDebugging

**種類:** DWORD

**値:** 1

前のセクションに表示されるレジストリ キーが作成され、ホスト プロセスが再起動されて後に、次のように、スクリプトをデバッグできます。

1. ホスト プロセスにデバッガーをアタッチします。 USB Bidi JavaScript では、これは spoolsv.exe です。

2. スクリプトのデバッグ モードには、デバッガーを設定します。

3. 次回のスクリプトの実行プロセスを中断するには、"Break All"(Ctrl + Alt + Break) を選択します。

4. 問題を再現するシナリオを実行します。

5. JavaScript 関数には、デバッガーが中断と必要なすべてのブレークポイントを設定、コードをステップ実行します。

## <a name="related-topics"></a>関連トピック

[双方向通信のスキーマ](bidirectional-communication-schema.md)  

[IPrinterBidiSchemaElement](iprinterbidischemaelement-interface.md)  

[IPrinterScriptContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)  

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  

[JavaScript API リファレンス](javascript-api-reference-.md)  

[印刷ドライバー USB モニターおよび双方向のサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)  

[USB の印刷](usb-printing.md)  

[V4 プリンター ドライバーの接続](v4-printer-driver-connectivity.md)



