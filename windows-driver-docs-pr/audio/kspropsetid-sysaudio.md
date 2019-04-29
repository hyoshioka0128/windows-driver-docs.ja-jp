---
title: KSPROPSETID\_Sysaudio
description: KSPROPSETID\_Sysaudio
ms.assetid: 817cbda5-9d37-4c12-8749-98a86540609f
keywords:
- KSPROPSETID_Sysaudio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bcc6fdd80274d2f73349c292fd11a339d5c2a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332452"
---
# <a name="kspropsetidsysaudio"></a>KSPROPSETID\_Sysaudio


## <span id="ddk_kspropsetid_sysaudio_ks"></span><span id="DDK_KSPROPSETID_SYSAUDIO_KS"></span>


`KSPROPSETID_Sysaudio`のプロパティにアクセスするプロパティ セットが使用される、 [SysAudio システム ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver)します。 Sysaudio はドライバーを管理する[仮想のオーディオ デバイス](https://msdn.microsoft.com/library/windows/hardware/ff538734)DirectSound およびその他のクライアントに代わってします。

SysAudio のクライアントは、このプロパティには、次の設定を使用します。

-   SysAudio のクライアントに利用できる仮想のオーディオ デバイスを列挙します。

-   SysAudio が仮想のオーディオ デバイスでインスタンス化できるピンを列挙します。

-   これらのピンの機能を決定します。

-   各ピンを流れるデータ ストリームのパスにあるノードを列挙します。

-   データの経路を含めるか、AEC のノードをバイパスする際に pin を構成します。

使用可能な仮想オーディオ デバイスのプロパティを表示するには、後にクライアントが仮想のオーディオ デバイスのいずれかを選択し、そのデバイスで pin を作成する準備があります。 一部のクライアントは、仮想のオーディオ デバイスでは、複数の pin を作成するか、1 つ以上のデバイスで pin を作成することができます。 ピンを作成する方法の詳細については、次を参照してください。 [Pin ファクトリ](https://msdn.microsoft.com/library/windows/hardware/ff537747)します。

クライアントが使用できる、暗証番号 (pin) を作成した後、 [KSPROPSETID\_Sysaudio\_Pin](kspropsetid-sysaudio-pin.md)暗証番号 (pin) を管理するプロパティに設定します。

次のプロパティのメンバーである、`KSPROPSETID_Sysaudio`プロパティ セット。

[**KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID**](ksproperty-sysaudio-component-id.md)

[**KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース**](ksproperty-sysaudio-create-virtual-source.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_名**](ksproperty-sysaudio-device-friendly-name.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_インターフェイス\_名**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY\_SYSAUDIO\_インスタンス\_情報**](ksproperty-sysaudio-instance-info.md)

[**KSPROPERTY\_SYSAUDIO\_選択\_グラフ**](ksproperty-sysaudio-select-graph.md)

 

 





