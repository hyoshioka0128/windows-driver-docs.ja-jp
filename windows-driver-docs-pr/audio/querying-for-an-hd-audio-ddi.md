---
title: HD オーディオ DDI のクエリ
description: HD オーディオ DDI のクエリ
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD オーディオ、クエリを実行します。
- 高解像度オーディオ (HD オーディオ) クエリを実行します。
- クエリの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e51aec944825b6a289ebfa11529f3739ef66f0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581654"
---
# <a name="querying-for-an-hd-audio-ddi"></a>HD オーディオ DDI のクエリ


関数のドライバー、オーディオまたはモデムのコーデックを送信します、HD オーディオ DDI を持つオブジェクトへの参照をカウントを取得する、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)HD オーディオ バス ドライバーに IOCTL します。

Windows Vista 以降では、HD オーディオ バス ドライバーのサポート、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)と[ **HDAUDIO\_バス\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418) DDI のバージョン。 サポートされていません、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)バージョン。

HD オーディオのバス ドライバーは、Windows Server 2003 および Windows XP でのアップグレードとしてインストールできます。 このバス ドライバーには、両方の DDI バージョンがサポートしています。

HDAUDIO への参照を取得するためのプロシージャ\_BUS\_インターフェイス、HDAUDIO\_BUS\_インターフェイス\_V2 および、HDAUDIO\_BUS\_インターフェイス\_DDI の BDL バージョンは次のセクションで説明します。

[取得、HDAUDIO\_BUS\_インターフェイス DDI オブジェクト](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[取得、HDAUDIO\_BUS\_インターフェイス\_V2 DDI オブジェクト](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[取得、HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクト](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




