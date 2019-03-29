---
title: ProcAmp コントロール用のデインターレース コンテナー デバイス
description: ProcAmp コントロール用のデインターレース コンテナー デバイス
ms.assetid: ce179efe-9e92-4407-8e90-896e4b9a2e84
keywords:
- コンテナー デバイス WDK DirectX VA
- デインター レースの WDK DirectX va なので、ProcAmp コントロール
- ProcAmp WDK DirectX va なので、コンテナー デバイス インター レースを解除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3357a55a9ca0edc9f24e89b44c28943a49eaca49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580380"
---
# <a name="deinterlace-container-device-for-procamp-control"></a>ProcAmp コントロール用のデインターレース コンテナー デバイス


## <span id="ddk_deinterlace_container_device_for_procamp_control_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_PROCAMP_CONTROL_GG"></span>


[ProcAmp コントロールの機能をサンプル](sample-functions-for-procamp-control.md)のため、最初に定義し、インター コンテナー デバイスを作成する必要がありますのみ、DirectX VA デバイスのコンテキスト内に使用できます。

[デインター レースのコンテナーのデバイスのインター レースを解除](deinterlace-container-device-for-deinterlacing.md)こともできます ProcAmp コントロール (この場合、ドライバーでは、ProcAmp 制御の調整をサポートしています)、ProcAmp コントロール デバイスの機能を確認します。 、サポートされている場合、ドライバーは、VMR はそのためには呼び出しを開始したときに ProcAmp コントロール デバイスを作成します。

**注**  インター コンテナー デバイスはソフトウェア コンス トラクターのみで、デバイス上に含まれている機能、ハードウェアを表していません。

 

 

 





