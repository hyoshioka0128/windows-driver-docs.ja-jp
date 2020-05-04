---
title: シリアルと Serenum の機能
description: シリアルと Serenum の機能
ms.assetid: 47202203-935a-4e1a-9b05-5555f7cbcfa8
keywords:
- シリアルデバイス WDK、シリアルドライバー
- シリアルデバイス WDK、Serenum.sys ドライバー
- シリアルドライバー WDK、シリアルドライバーについて
- Serenum.sys ドライバー WDK、Serenum.sys ドライバーについて
- Serial service WDK
- シリアルドライバー WDK
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7a123eaf5e6074d90cc3ce7b0f9f06bf19723e4b
ms.sourcegitcommit: 6b09412f7bf562f7c01ffa94ac44a3d0ea895e3c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086724"
---
# <a name="features-of-serial-and-serenum"></a>シリアルと Serenum の機能





Windows 2000 以降、システムによって提供されるシリアルコントローラーデバイスを管理できるようになりました。このドライバーは、16550 universal 非同期レシーバー (UART) と互換性のあるハードウェアインターフェイスを備えています。 シリアル .sys は、スタンドアロンのシリアルポート、COM ポート、およびマルチポートボードを制御します。 Serenum.sys は、serial .sys または互換性のあるシリアルドライバーによって制御されるシリアルポートに接続されているデバイスを列挙します。

シリアルとシリアルフレームワークの拡張機能 (SerCx2 と SerCx) との比較については、「[シリアルコントローラードライバーの概要](serial-drivers-overview.md)」を参照してください。 SerCx2 は、Windows 8.1 から使用できます。 SerCx は Windows 8 以降で使用できます。

シリアルはシリアルサービスを実装します。実行可能イメージは、Serial. sys です。

Serial は次のように使用されます。

-   レガシおよびプラグアンドプレイシリアルデバイス用の関数ドライバー。

-   16550 UART 互換インターフェイスを必要とするプラグアンドプレイデバイス用の下位レベルのデバイスフィルタードライバー。 この構成の例として、 [PCMCIA バス](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/)上のモデムがあります。

    フィルタードライバーとしてのシリアル操作は、関数ドライバーと同じ操作と同じです。

シリアル機能は次のとおりです。

-   プラグアンドプレイ、電源管理、および Windows Management Instrumentation (WMI)。

-   シリアルを含むシリアルデバイススタックの電源ポリシー所有者。

-   スタンドアロンのシリアルポート、 [COM ポート](configuration-of-com-ports.md)、マルチポートボードの数に制限はありません。

-   割り込みと、デバイスハードウェアとの通信を制御します。

Serenum.sys は、Serenum.sys サービスを実装します。実行可能イメージは Serenum.sys です。

Serenum.sys は、シリアルポート関数ドライバーと共に使用される上位レベルのデバイスフィルタードライバーで、シリアルポートに接続されている次の種類のデバイスを列挙します。

-   *プラグアンドプレイ外部 COM デバイス仕様 (バージョン1.00、1995年2月28日*) に準拠しているシリアルデバイスプラグアンドプレイます。

-   Microsoft Windows NT 4.0 およびそれ以前のバージョンでのレガシマウスの検出に準拠しているポインターデバイス。

Serial と Serenum.sys の組み合わせ操作は、シリアルポート用のプラグアンドプレイバスドライバーの機能を提供します。

Serenum.sys はプラグアンドプレイと電源管理をサポートしています。

Serenum.sys は Windows Driver Model をサポートしておらず、Windows 2000 以降のバージョンでのみ使用する必要があります。

Windows 2000 以降では、シリアルポートを列挙する必要があるシリアルポートとその他のシリアルポート関数ドライバーがサポートされています。 ハードウェアベンダーは、シリアルポート用に独自の列挙子を作成する必要はありません。 たとえば、デバイスドライバーは、Serenum.sys を使用して、マルチポートデバイス上の個々のシリアルポートに接続されているデバイスを列挙できます。

 

 




