---
title: 全二重モード
description: 全二重モード
ms.assetid: 01e3388d-d568-4476-9ff0-2125acafb841
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6f67645c7a03f4e25e5c51910e1da13453f5a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579799"
---
# <a name="full-duplex-mode"></a>全二重モード


## <span id="ddk_full_duplex_mode_kg"></span><span id="DDK_FULL_DUPLEX_MODE_KG"></span>


Storport ドライバーには、高パフォーマンスのバスに特化した I/O モデルをサポートしています。 この I/O モデルでは、ミニポート ドライバーに追加、新しい要求がキュー場合でも、他のユーザーの完了の場合は、つまり、全二重モードで動作するミニポート ドライバーを許可します。 さらに、全二重モード、ミニポート ドライバーがの実行を同期するその[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)割り込みサービス ルーチンとします。 これは、大幅なパフォーマンスの向上につながります。 ただし、Storport は、既定では、半二重モードで動作するためのミニポート ドライバーを全二重モードで活用するために設計する必要があります。

ミニポート ドライバーが Storport の実行中に、全二重モードで動作するを構成する必要があります、 [ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)ルーチン。 これは、初期化して、 **SynchronizationModel**のミニポート ドライバーのメンバー [**ポート\_構成\_情報 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)構造体を**StorSynchronizeFullDuplex**します。

 

 




