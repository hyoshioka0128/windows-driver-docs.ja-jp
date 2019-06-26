---
title: ログの記録
ms.assetid: CB7FE988-6E5A-4669-9FFB-A2B3F8DAF30F
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: 関数やメソッド、NCI パケット/プロトコル、およびその他の詳細なログ記録の NFC ログを記録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf627fd102ebf04e36d01296e70efd718ecbeed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375112"
---
# <a name="logging"></a>ログの記録


関数またはメソッドと、その他の詳細ログ記録の*Windows ソフトウェア トレース プリプロセッサ*(WPP) ログを使用します。 NCI パケット/プロトコルのログ記録、Event Tracing for Windows (ETW) を使用します。 WPP デバッグのログ記録を有効にするには、次のコマンドを使用します。

```cpp
tracelog -start MyNfcSession -f C:\Data\test\bin\MyNfcSession.etl
tracelog -enableex MyNfcSession -guid #351734b9-8706-4cee-9247-04accd448c76 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #696D4914-12A4-422C-A09E-E7E0EB25806A -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #9d97cb90-8dee-42b8-b553-d1816be6fb9e -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #4EB7CC58-145C-4a79-9418-68CD290DD9D4 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #D976D933-B88B-4227-95F8-00513C0986DE -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -stop MyNfcSession
```

これは、c: MySession.etl という名前の ETL ファイルを生成\\データ フォルダー。 それらをデコードすることができますしを使用して[Tracepdb](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb) (Tracepdb.exe) と[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt) (Tracefmt.exe)、Windows ドライバー キットに含まれています。

NFC CX では、すべてのデバッグ拡張機能は含まれません。

## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[Event Tracing for Windows (Windows ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-software-tracing)  
[ソフトウェア トレース用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
