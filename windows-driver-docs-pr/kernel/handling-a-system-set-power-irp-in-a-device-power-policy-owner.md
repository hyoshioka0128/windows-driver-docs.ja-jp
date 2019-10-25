---
title: デバイス電源ポリシー所有者のシステム電源設定 IRP の処理
description: デバイス電源ポリシー所有者のシステム電源設定 IRP の処理
ms.assetid: f6206455-142b-4f3f-ae5a-d8e79386bce3
keywords:
- パワー Irp WDK 電源管理の設定
- デバイスの電源ポリシー所有者 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6f471152bd518fdd52f9944b221c99d09f2078
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836613"
---
# <a name="handling-a-system-set-power-irp-in-a-device-power-policy-owner"></a>デバイス電源ポリシー所有者のシステム電源設定 IRP の処理





システム設定-電源 IRP への応答として、デバイススタックの[電源ポリシー所有者](managing-device-power-policy.md)は、デバイススタックを適切なデバイスの電源状態にする役割を担います。

一般的なルールとして、デバイスの電源ポリシー所有者は、システム電源状態の[ **\_電源\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された irp\_を受け取ると、システム設定-電源 IRP をデバイススタックに渡すことによって応答する必要があります。 また、デバイスの電源ポリシーの所有者は、デバイススタックの IRP を\_に送信し、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンで対応するデバイスの電源状態を **\_電力\_設定**することによって応答する必要があります。 スタック内のすべてのドライバーがデバイスセット-電源 IRP を完了すると、デバイスの電源ポリシー所有者はシステム設定-電源 IRP を完了します。

ただし、システム再開のパフォーマンスを向上させるために、子デバイスを持たないデバイスのデバイス電源の所有者は、[スリープ状態](system-sleeping-states.md)からの[作業状態 S0](system-working-state-s0.md)にシステムが戻るまでにかかる時間を短縮するために、別のアプローチを使用する必要があります。 この場合、システムを動作状態 S0 に返すシステムセット-電源 IRP への応答として、デバイスの電源ポリシー所有者は次の一連の操作を実行する必要があります。

1.  **Irp\_の\_** を受信した後、ドライバーの[DispatchPower ルーチン](dispatchpower-routines.md)で S0 システムの電源状態に\_電源 irp を設定し、irp の*iocompletion*ルーチンを設定して、irp をスタックに渡します。

2.  手順 (1) で設定された*Iocompletion*ルーチンで、irp\_が完了したことを要求し、対応するデバイスの電源状態に **\_電源 irp\_設定**してから、システムセット-電源 irp を直ちに完了します。 ドライバーは、システム設定-電源 IRP を完了する前に、デバイスセット-電源 Irp が完了するのを待機することはできません。 すべての下位レベルのドライバーがシステム設定-電源 IRP を完了し、システム設定-電源 IRP がドライバーの機能デバイスオブジェクト (FDO) に渡されると、 *Iocompletion*ルーチンが実行されます。

3.  デバイス固有の必要な初期化を実行します。

4.  手順 (2) で送信されたデバイスセット-電源 IRP を完了します。

5.  デバイスが[スリープ状態](device-sleeping-states.md)のときにキューに登録された i/o 要求を処理します。

カーネルパワーマネージャーには、一部の IRP dispatch キューが含まれており、システムの動作状態 S0 に戻るまで、すべてのデバイスに迅速に通知する必要があります。 システム設定-電源 IRP を可能な限り迅速に完了できないドライバーは、システムの電源状態遷移中のシステム全体のパフォーマンスに悪影響を及ぼす可能性があるシステム設定-電源 IRP を他のデバイスから取得できないようにします。

システム設定-電源 Irp の処理の詳細については、次を参照してください。

[デバイスの電源状態が正しいことを確認する](determining-the-correct-device-power-state.md)

[デバイスセットの送信-システムセットへの応答としての電源 IRP-電源 IRP](sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp.md)

 

 




