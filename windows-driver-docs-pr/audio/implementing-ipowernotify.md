---
title: IPowerNotify の実装
description: IPowerNotify の実装
ms.assetid: 8bd8b4c8-1961-41ea-ba98-41e3a732ed37
keywords:
- IPowerNotify インターフェイス
- 通知 WDK オーディオ
- 電源状態の変更通知の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccd4decdec6ff9322a576f227580fcb468656c6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833233"
---
# <a name="implementing-ipowernotify"></a>IPowerNotify の実装


## <span id="implementing_ipowernotify"></span><span id="IMPLEMENTING_IPOWERNOTIFY"></span>


ドライバーのミニポートオブジェクト ([オーディオミニポートオブジェクトインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-miniport-object-interfaces)を参照) またはストリームオブジェクト (「[オーディオストリームオブジェクトインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-stream-object-interfaces)」を参照) が電源状態の変更について知る必要がある場合は、 **QueryInterface**メソッドで[ipowernotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)インターフェイスをサポートし、電源変更が発生するたびに PortCls システムドライバーから通知を受け取ることができます。

電源状態が変化すると、PortCls は[**ipowernotify::P owerchangenotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-ipowernotify-powerchangenotify)メソッドを呼び出して、 **ipowernotify**インターフェイスをサポートする各ミニポートおよびストリームオブジェクトを個別に通知します。 **PowerChangeNotify**の呼び出し中に、ミニポートオブジェクトが新しいデバイスの電源状態をキャッシュする必要があります。 **Cadaptercommon:: Init**の呼び出し中に (たとえば、Microsoft Windows Driver KIT \[WDK\])、ミニポートドライバーは、キャッシュされた電源状態を初期値 PowerDeviceD0 に設定する必要があります.

**PowerChangeState**を呼び出して電源を切る前に、PortCls は**ipowernotify::P owerchangenotify**を呼び出して、ミニポートドライバーに必要なデバイスコンテキストを保存する機会を与えます。 このコンテキストには、現在のフィルタートポロジとミキサーライン設定を具体化したハードウェアレジスタ値が含まれる場合があります (たとえば、)。 **PowerChangeState**を呼び出して電源を入れた後、PortCls は**PowerChangeNotify**を呼び出して、ミニポートドライバーが保存されたコンテキストを復元できるようにします。

電源を切ると、PortCls は、 **PowerChangeNotify**を呼び出す前に、アクティブなオーディオデータストリームを一時停止します。 PortCls は、電源をオンにすると、一時停止しているオーディオデータストリームを再起動する前に**PowerChangeNotify**を呼び出します。

ミニポートドライバーのミニポートおよびストリームオブジェクトクラスは、 **Ipowernotify**インターフェイスから継承でき、 **NonDelegatingQueryInterface**メソッドでこのインターフェイスをサポートします。 ヘッダーファイル Portcls からの IMP\_IPowerNotify 定義を使用して、 **PowerChangeNotify**メソッドの関数宣言を、ドライバーのミニポートオブジェクトとストリームオブジェクトのクラス定義に追加できます。

 

 




