---
title: Wi-Fi Direct 印刷
description: Windows 8.1 以降のバージョンの Windows では、Wi-fi Direct (WFD) を介した印刷がサポートされています。
ms.assetid: B2FC1293-F9E4-43A4-84BF-21EF8C3D27E0
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: e5047730ad7ba5a80785ff4b654c5b55e606c19b
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793738"
---
# <a name="wi-fi-direct-printing"></a>Wi-Fi Direct 印刷

Windows 8.1 以降のバージョンの Windows では、Wi-fi Direct (WFD) を介した印刷がサポートされています。

Windows Wi-fi Direct サポートを実装する印刷デバイスは、次のものを実装する必要があります。

- Wi-fi Direct の垂直方向のペアリング

- 物理デバイス内のすべての論理デバイスに一致するコンテナー ID

- WSD/WS 印刷

このトピックとサブトピックで使用される定義:

| 用語 | 説明 |
|--|--|
| WFD | Wi-Fi Direct |
| DAF | デバイスの関連付けフレームワーク |
| DAS | デバイス関連付けサービス |
| GO | グループの所有者 |
| PBC | プッシュボタン接続 |

Wi-fi direct 印刷のサポートに関する一般的な情報については、「 [Wi-fi Direct 印刷の概要](wfd-overview.md)」を参照してください。 Wi-fi Direct 印刷を実装する方法の詳細については[、「Wi-fi Direct 印刷の実装](wfd-implementation.md)」を参照してください。

## <a name="certification-requirements"></a>認定の要件

この機能に関連付けられている新しい証明書の要件はありません。 該当する既存の要件については、以下の[関連ドキュメント](#related-documents)を参照してください。

## <a name="hck-requirements"></a>HCK の要件

デバイスは、wi-fi Direct の wi-fi アライアンス認定を持っている必要があります (実装されている場合)。

印刷デバイスの既存のすべての認定要件は、使用可能なすべてのトランスポートで適用可能な HCK テストを実行するための要件も含めて適用されます。 変更がある場合、パートナーは、Windows 認定チームによって発行された公式の認定要件ドキュメントを常に参照する必要があります。

> [!NOTE]
> Wi-fi アライアンス認定の要件は Wi-fi ダイレクト用です。 Wi-fi アライアンス Wi-fi Direct サービスは別の仕様であり、現時点では Windows ではサポートされていません。

## <a name="related-documents"></a>関連ドキュメント

[コンテナー ID の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)

[PnP-X: Windows 仕様のプラグアンドプレイ拡張機能](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))

[Wi-fi アライアンス-wi-fi Direct 業界ホワイトペーパー](https://www.wi-fi.org)
