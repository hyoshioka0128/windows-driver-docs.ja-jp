---
title: COM ポートの構成
description: COM ポートの構成
ms.assetid: 519ca9c8-bc67-4a85-87ae-6015c6212dea
keywords:
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f94f917f6b9e3606675a560edae0318ceb1ad1
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836338"
---
# <a name="configuration-of-com-ports"></a>COM ポートの構成

Windows 2000 以降、COM ポートは、次の要件に準拠するシリアル ポートの種類を示します。

- COM ポートは、COM ポートのデバイスのインターフェイス クラスのインスタンスを通じてアクセスします。 このクラスの GUID が GUID\_DEVINTERFACE\_Ntddser.h で定義されている com ポート。

- COM ポートを操作するには、Ntddser.h で定義されている 16550 UART と互換性のあるインターフェイスを使用できます。

- COM にアクセスするほとんどのアプリケーションとの互換性をポートに確実には、標準的な名前付け規則を使用するシンボリック リンクの名前を割り当てる必要があります"COM<em>&lt;n&gt;</em>"ここで、 *&lt;n&gt;* COM ポート番号 (COM1 など) です。 COM を使用する場合<em>&lt;n&gt;</em> 名、COM ポート番号を取得する必要があります *&lt;n&gt;* から、 [COM ポート データベース](com-port-database.md). COM ポート番号は、COM でのみ使用する必要があります<em>&lt;n&gt;</em> 名。

既定でポートのクラスのインストーラーの結合操作[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)シリアル関数ドライバーは、COM ポートとしてデバイスを構成するとします。

ポート クラスのインストーラーとシリアルの COM ポートの COM ポート デバイス インターフェイスを作成する方法については、次を参照してください。[外部名前付けの COM ポート](external-naming-of-com-ports.md)します。
