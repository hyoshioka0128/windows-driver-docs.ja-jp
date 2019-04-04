---
title: 携帯電話の COM API の設計ガイド
description: このセクションでは、携帯電話の COM API についてを説明します。
ms.assetid: 93aa20d0-d8c3-40ec-baf1-fab56ff5686d
keywords:
- 携帯電話の COM API の設計ガイド ネットワーク ドライバー
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da7aa11d0d6e2b5d35a87d593cdd8aa3ba965f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530849"
---
# <a name="cellular-com-api-design-guide"></a>携帯電話の COM API の設計ガイド

> [!WARNING]
> 携帯電話の COM API は、Windows 10 で非推奨とされます。 このコンテンツは、OEM および携帯電話会社が Windows Phone 8.1 アプリケーションの作成の保守をサポートするために提供されます。

このセクションでは、携帯電話の COM API についてを説明します。

Microsoft インターフェイス定義言語 (MIDL) の 2 つのファイルでは、インターフェイスが用意されています。

- cellularapi_oem.idl
- rilapitypes.idl

ヘッダー ファイルを生成するのにには、MIDL コンパイラを使用します。 詳細については、[Microsoft インターフェイス定義言語](https://msdn.microsoft.com/library/windows/desktop/aa367091)、Windows デベロッパー センターでを参照してください。

携帯電話アプリケーションを含むパッケージ内の適切な機能を宣言する必要があります。 詳細については、[携帯電話の COM API 機能](cellular-com-api-capabilities.md)を参照してください。

## <a name="in-this-section"></a>このセクションの内容

[携帯電話の COM API の機能](cellular-com-api-capabilities.md)

[IOemCellularModem インターフェイスを使用して、RIL ドライバーとの通信します。](communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface.md)

## <a name="related-topics"></a>関連トピック

[携帯電話の COM API リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn946508)

