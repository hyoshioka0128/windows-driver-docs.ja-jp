---
title: IPowerNotify の実装
description: IPowerNotify の実装
ms.assetid: 8bd8b4c8-1961-41ea-ba98-41e3a732ed37
keywords:
- IPowerNotify インターフェイス
- 通知の WDK オーディオ
- 電源状態変更通知の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 559b830207ff7a65025910eb8207b3e4678e7a1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359899"
---
# <a name="implementing-ipowernotify"></a>IPowerNotify の実装


## <span id="implementing_ipowernotify"></span><span id="IMPLEMENTING_IPOWERNOTIFY"></span>


場合、ドライバーのミニポート オブジェクト (を参照してください[オーディオ ミニポート オブジェクト インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-miniport-object-interfaces)) またはオブジェクトをストリーム (を参照してください[オーディオ Stream オブジェクト インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-stream-object-interfaces))、をサポートする電源状態の変更について知っておく必要があります[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipowernotify)インターフェイスでその**QueryInterface**メソッドと電源の変更が発生するたびに、PortCls システム ドライバーからの通知を受信します。

電源状態の変更、PortCls を呼び出すと、 [ **IPowerNotify::PowerChangeNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-ipowernotify-powerchangenotify)オブジェクトをサポートするのに個別に各ミニポートとストリームを通知するメソッド、 **IPowerNotify**インターフェイス。 中に、 **PowerChangeNotify**を呼び出すと、ミニポート オブジェクトは、新しいデバイスの電源状態をキャッシュする必要があります。 中に、 **CAdapterCommon::Init**呼び出し (たとえば、Microsoft Windows ドライバー キット Msvad サンプル アダプターの実装を参照してください\[WDK\])、ミニポート ドライバーは、キャッシュされた電源状態を設定する必要がありますPowerDeviceD0 初期値。

呼び出しの前に**PowerChangeState**電源、PortCls 呼び出しを**IPowerNotify::PowerChangeNotify**ミニポート ドライバーに任意の必要なデバイス コンテキストを保存する機会を提供します。 このコンテキストには、たとえば現在フィルター トポロジとミキサー行の設定を具現化するハードウェア レジスタの値が含まれます。 呼び出した後**PowerChangeState** PortCls 呼び出しの電源を投入**PowerChangeNotify**ミニポート ドライバーが保存されたコンテキストを復元できるようにします。

PortCls に呼び出す前に、アクティブなオーディオ データ ストリームが一時停止、電源と**PowerChangeNotify**します。 電源投入 PortCls 呼び出し**PowerChangeNotify**オーディオ データ ストリームを一時停止、再起動する前にします。

ミニポート ドライバーのミニポートおよびストリーム オブジェクトのクラスから継承できます、 **IPowerNotify**インターフェイスし、では、このインターフェイスをサポート、 **NonDelegatingQueryInterface**メソッド。 実装を使用する\_ヘッダー ファイルの関数の宣言を追加する Portcls.h から IPowerNotify 定義、 **PowerChangeNotify**ドライバーのミニポートおよびストリーム オブジェクトのクラス定義にメソッド。

 

 




