---
title: デバイス レベルの温度管理
description: Windows 8 以降、Windows は、カーネル モード デバイス ドライバーのデバイス レベルの温度管理をサポートします。
ms.assetid: C66E0050-04E8-4DCD-B989-94A97558C4CE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b87b6df95ad96524d886eb65ec3f230143f72978
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385013"
---
# <a name="device-level-thermal-management"></a>デバイス レベルの温度管理


Windows 8 以降、Windows は、カーネル モード デバイス ドライバーのデバイス レベルの温度管理をサポートします。 Windows の温度管理では、これらの目標があります。

-   正しくないか含んでを操作することがあります、過熱状態からのハードウェア プラットフォームでのデバイスをできないようにします。
-   コンピューター ケースにユーザーがアクセスできるサーフェスを過快適タッチまたは保持することを回避します。

温度のグローバル条件のコンテキストでローカル デバイスの温度の制約を調整することにより、プラットフォーム全体でと同様に、電源管理、温度管理を実装しなければなりません。 グローバルな調整を提供するには、オペレーティング システムは、ユーザーが実行しているタスクへの干渉を最小限に抑える方法で複数のデバイスで冷却に関する要件を配布できます。 温度要件は、電源管理とユーザーの操作に対する応答性などの他のシステム要件をインテリジェントに分散できます。

一方、プラットフォームで他のデバイスからの分離でローカルに、そのデバイスの温度のレベルを管理しようとするデバイス ドライバーは、非効率的な電力使用状況と、応答していないユーザー インターフェイス (UI) と、不適切な判断をする可能性が高くなります。

デバイス ドライバーを実装するグローバルの温度管理に参加するには[GUID\_熱\_冷却\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh698265)ドライバー インターフェイス。 システムの起動時には、Acpi.sys、システム指定のドライバーは、システムにはこのインターフェイスをサポートすると、それらの特定のデバイス ドライバーを照会します。 ドライバーが表示されることができます、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)後にいつでもこのインターフェイスの要求、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ドライバーのデバイスのルーチンが呼び出されます。 この要求に応答してでは、温度管理機能を備えているデバイスのドライバーがへのポインターを提供できます、 [**熱\_冷却\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/hh698275)構造体。 この構造体には、ドライバーによって実装されるコールバック ルーチンのセットへのポインターが含まれています。 デバイスの温度のレベルを管理するには、は、オペレーティング システムは、これらのルーチンを直接呼び出します。

このインターフェイスで 2 つのプリンシパル ルーチンは[ *ActiveCooling* ](https://msdn.microsoft.com/library/windows/hardware/hh698235)と[ *PassiveCooling*](https://msdn.microsoft.com/library/windows/hardware/hh698270)します。 ドライバーの*ActiveCooling*ルーチンが関与します。 または、デバイスのアクティブな冷却を解除します。 たとえば、このルーチンはオンとオフをファンをする場合があります。 ドライバーの*PassiveCooling*ルーチンは、先には、許容可能な温度レベルを維持するために、デバイスのパフォーマンスを調整度を制御します。 たとえば、過熱状態を防ぐために、半分の速度でデバイスを実行するこのルーチンを呼び出す可能性があります。

既定では、最初の呼び出しの前に、 *ActiveCooling*作動は日常的なアクティブな冷却 (たとえば、ファンが電源オフ)。 最初の呼び出しの前に、 *PassiveCooling* 、日常的な冷却制限なしで最大限のパフォーマンスで実行するデバイスは、ドライバーに構成します。

ドライバーは、デバイスのハードウェアの機能によって、これらのルーチンの一方または両方を実装できます。 詳細については、次を参照してください。[パッシブ、アクティブな冷却モード](passive-and-active-cooling-modes.md)します。

 

 




