---
Description: サポートされるシナリオ
title: サポートされるシナリオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1464cc6eb3bc4b10b66ed900a61a328efaa4647
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380859"
---
# <a name="supported-scenarios"></a>サポートされるシナリオ


Windows ポータブル デバイス (WPD) DDI には、デバイスの内容、デバイスの動作を制御、および enabe 垂直ソリューションを参照するか、デバイスからコンテンツを転送することができます。 このセクションでは、これらの各シナリオについて説明します。

## <a name="span-idcontenttransferspanspan-idcontenttransferspanspan-idcontenttransferspancontent-transfer"></a><span id="Content_Transfer"></span><span id="content_transfer"></span><span id="CONTENT_TRANSFER"></span>コンテンツの転送


WPD には、アプリケーションと Windows を実行しているコンピューターに接続されているポータブル デバイス間のデータ転送を標準化するために必要なインフラストラクチャが用意されています。 これは、デバイスとデータにアクセスして転送する、コンテンツと標準化されたメカニズムの統一されたビューでアプリケーションを提供します。

たとえば、WPD DDI は、デバイスとコンピューター間でコンテンツを同期するアプリケーションを使用できます。

## <a name="span-idbrowsingdevicecontentsspanspan-idbrowsingdevicecontentsspanspan-idbrowsingdevicecontentsspanbrowsing-device-contents"></a><span id="Browsing_Device_Contents"></span><span id="browsing_device_contents"></span><span id="BROWSING_DEVICE_CONTENTS"></span>デバイスの内容を参照


WPD 名前空間を使用すると、ユーザーは、任意の型のポータブル デバイスを Windows ファイルの管理方法を適用できます。 (WPD アプリケーションでのコンテキスト メニューとプロパティ ページの拡張機能を実装する方法の詳細については、Windows ポータブル デバイスのプログラミングの番組ガイドを参照してください、 [WPD SDK](https://go.microsoft.com/fwlink/p/?linkid=178695))。

## <a name="span-iddevicecontrolspanspan-iddevicecontrolspanspan-iddevicecontrolspandevice-control"></a><span id="Device_Control"></span><span id="device_control"></span><span id="DEVICE_CONTROL"></span>デバイスの制御


デバイスのコンテンツを標準のアクセスを提供するだけでなく、WPD インフラストラクチャには、デバイスのコントロールを標準化する方法が用意されています。 これにより、さまざまなデバイスの動作を制御できるだけでなく、デバイス コマンドを発行するアプリケーション。 たとえば、携帯電話用 WPD アプリケーションは、電話のメッセージの送信を要求またはコンピューターに接続されているときにメッセージが表示されます。

## <a name="span-idenablingverticalsolutionsspanspan-idenablingverticalsolutionsspanspan-idenablingverticalsolutionsspanenabling-vertical-solutions"></a><span id="Enabling_Vertical_Solutions"></span><span id="enabling_vertical_solutions"></span><span id="ENABLING_VERTICAL_SOLUTIONS"></span>垂直方向のソリューションを有効にします。


WPD インフラストラクチャでは、高い拡張性を備えたデバイスの表現と制御のメカニズムを提供します。 これにより、垂直方向のソリューション プロバイダー WPD アプリケーション プログラミング インターフェイス (API) を使用して、標準化された WPD の外部で設定される強化されたユーザー エクスペリエンスを作成します。 この例には、デバイス、ファームウェアの更新プログラム、およびデバイス (リモート サポート) 用の診断情報に含まれているベンダーが提供するソフトウェア スイートが含まれます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





