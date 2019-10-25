---
title: ログ
ms.assetid: CB7FE988-6E5A-4669-9FFB-A2B3F8DAF30F
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: NFC は、関数/メソッド、NCI パケット/プロトコル、およびその他の詳細ログをログに記録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdefeb5dd08f8b8cb816738df50d72bca510f87d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842740"
---
# <a name="logging"></a>ログ


関数/メソッドとその他の詳細ログについては、 *Windows software trace プリプロセッサ*(WPP) のログ記録が使用されます。 NCI パケット/プロトコルのログ記録では、Windows イベントトレーシング (ETW) が使用されます。 デバッグのために WPP ログ記録を有効にするには、次のコマンドを使用します。

```cpp
tracelog -start MyNfcSession -f C:\Data\test\bin\MyNfcSession.etl
tracelog -enableex MyNfcSession -guid #351734b9-8706-4cee-9247-04accd448c76 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #696D4914-12A4-422C-A09E-E7E0EB25806A -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #9d97cb90-8dee-42b8-b553-d1816be6fb9e -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #4EB7CC58-145C-4a79-9418-68CD290DD9D4 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #D976D933-B88B-4227-95F8-00513C0986DE -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -stop MyNfcSession
```

これにより、C:\\データフォルダーに MySession という名前の ETL ファイルが生成されます。 その後、 [tracepdb](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb) (tracepdb) と[tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt) (tracefmt) を使用してデコードできます。このファイルは、Windows Driver Kit に含まれています。

NFC CX には、デバッグ拡張機能は含まれていません。

## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[Windows イベントトレーシング (Windows ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-software-tracing)  
[ソフトウェア トレース用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
