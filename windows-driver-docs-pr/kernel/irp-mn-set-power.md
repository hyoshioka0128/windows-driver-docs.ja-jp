---
title: IRP_MN_SET_POWER
description: この IRP 通知システムの電源状態が変更されたドライバーまたはデバイスのデバイスの電源状態を設定します。
ms.date: 08/12/2017
ms.assetid: 1294183a-bd0b-4ead-bd64-669d5b3725ce
keywords:
- IRP_MN_SET_POWER カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 220924dd1997ca425f5173b2b90d507560ecf496
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582385"
---
# <a name="irpmnsetpower"></a>IRP\_MN\_設定\_電源


この IRP 通知システムの電源状態が変更されたドライバーまたはデバイスのデバイスの電源状態を設定します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_POWER** ](irp-mj-power.md)送信されるときに
---------

システム電源マネージャーまたはデバイスの電源ポリシー所有者は、この IRP を送信できます。

電源マネージャーは、システムの電源状態が変更されたドライバーに通知するには、この IRP を送信します。 ドライバーには、アイドル状態の検出には、そのデバイスが登録されているが、電源マネージャはアイドル状態のデバイスの電源状態を変更するには、この IRP を送信します。

電源ポリシーを所有しているドライバーでは、そのデバイスのデバイスの電源状態を設定するには、この IRP を送信します。 ドライバーを呼び出す必要があります[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)この IRP を送信します。

電源マネージャー IRQL でこの IRP の送信 = パッシブ\_レベル設定デバイス スタックを\_POWER\_pdo PAGABLE フラグを設定します。 このようなスタック内のドライバーは、要求を完了するページ コードまたはデータにタッチします。

電源マネージャーは IRQL で IRP を送信することができます = ディスパッチ\_レベルの場合、操作を行います\_POWER\_突入フラグを設定します。 このようなドライバー直接的または間接的にアクセスできません、ページのコードやデータ。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.Power.Type**メンバーか、設定されている電源状態の種類を指定する**SystemPowerState**または**DevicePowerState**します。

**Parameters.Power.State**メンバー自体には、電源の状態を次のように指定します。

-   場合**Parameters.Power.Type**は**SystemPowerState**、値の列挙子は、 [**システム\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff564565)型。

-   場合**Parameters.Power.Type**は**DevicePowerState**、値の列挙子は、 [**デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff543160)型。

**Parameters.Power.ShutdownType**メンバーが要求された移行に関する追加情報を指定します。 このメンバーの値には**POWER\_アクション**列挙値。 詳細については、次を参照してください。[システム電源操作](https://msdn.microsoft.com/library/windows/hardware/ff564553)します。

以降、Windows Vista では、 **Parameters.Power.SystemPowerStateContext**メンバーは読み取り専用で、部分的に非透過的な[**システム\_POWER\_状態\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/jj835780)コンピューターの前のシステム電源の状態に関する情報を含む構造体。 場合**Parameters.Power.Type**は**SystemPowerState**と**Parameters.Power.State**は**PowerSystemWorking**、2 つのフラグでは、このビット構造体は、高速スタートアップまたは休止からのスリープ解除、S0 を入力するコンピューターの原因となったかどうかを示す (作業) システムの状態。 詳細については、次を参照してください。[区別高速スタートアップ ウェイク-から-休止状態から](https://msdn.microsoft.com/library/windows/hardware/jj835779)します。

## <a name="output-parameters"></a>出力パラメーター


**Parameters.Power.SystemContext**システム用に予約されています。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_をデバイスが要求された状態を入力したことを示すために成功します。

ドライバーでは、システムの電源状態を設定する要求は失敗する必要があります。

バス ドライバーの上に配置されている関数とフィルター ドライバーでは、デバイスの電源状態を設定する要求は失敗する必要があります。 デバイスが削除された場合、または削除処理中、バス ドライバーは、デバイスの電源を要求にフェールバックできます。

<a name="operation"></a>操作
---------

電源マネージャーまたはドライバーが要求することができます、 **IRP\_MN\_設定\_POWER** IRP します。 電源マネージャーは、次の理由の 1 つのこの IRP を送信します。

-   システム電源の状態が変更されたドライバーに通知するには

-   電源マネージャーがアイドル状態の検出を実行するデバイスの電源状態を変更するには

電源ポリシーがデバイスを所有しているドライバーの送信**IRP\_MN\_設定\_POWER**にそのデバイスの電源状態を変更します。

任意の時点でデバイス オブジェクトごとにアクティブにするこのような 1 つだけの IRP が許可されます。

各ドライバーは、呼び出すことによって、次の下位ドライバーまで各電源 IRP を渡す必要があります[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (Windows Vista 以降) または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)(Windows Server 2003、Windows XP、および Windows 2000)。 **PoCallDriver**インターフェイスは、以下のこと**保留**、電源管理サブシステムは、次のドライバーに渡す前に、IRP を遅らせることができます。 遅延が発生など、 **PowerDeviceD0**要求、デバイスが突入電流が必要ですし、したがって電源必要がありますを逐次的にこのような別のデバイスとかどうか。

ドライバーを受信した後、 **IRP\_MN\_設定\_POWER**ドライバーを呼び出す必要がありますに対して要求を Windows server 2003、Windows XP、または Windows 2000 [ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)」の説明に従って、[呼び出す PoStartNextPowerIrp](https://msdn.microsoft.com/library/windows/hardware/ff540724)します。 Windows Vista 以降、通話**PoStartNextPowerIrp**は必要ありませんし、このような呼び出しには電源管理操作は実行されません。

**IRP\_MN\_設定\_システム電源の状態の電源**

システム電源マネージャーは、システムを送信できますのみ IRP の出力を設定します。

ドライバーでは、システムの電源状態を設定する要求は失敗する必要があります。

電源マネージャーに送信可能であれば、 [ **IRP\_MN\_クエリ\_POWER** ](irp-mn-query-power.md)送信する前に**IRP\_MN\_設定\_POWER**システムのスリープ状態を要求します。 ただし、いくつかの条件下 (ユーザー キーを押してなど、**電源オフ**ボタンや、バッテリの期限切れ)、電源マネージャーが発行**IRP\_MN\_設定\_POWER**最初のクエリを使用しません。 スリープ状態にのみ電源マネージャーのクエリ電源を投入する前に決してを照会します。

**IRP\_MN\_設定\_POWER**要求は、デバイスのデバイス スタックの最上位のドライバーに送信されます。 上のドライバーは、IRP IRP を完了する必要があります、バス ドライバーに到達するまで、[次へ] の下位のドライバーに IRP を渡します。

フィルター ドライバーがシステムで動作する必要はない通常セット power IRP 渡す以外の場合。

ただし、デバイスの電源ポリシー所有者を設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP を渡す前に日常的な。 *IoCompletion*日常的な送信、 **IRP\_MN\_設定\_POWER** IRP のデバイスの電源を要求します。 詳細については、次を参照してください。[電源ポリシー所有者のデバイスでシステム セット Power IRP の処理](https://msdn.microsoft.com/library/windows/hardware/ff546749)します。

システム設定 power IRP は、システムの電源状態の変更が近づいていることと、ドライバーの準備する必要がありますにドライバーを通知します。 ただし、ドライバーを変更しないでください、デバイスの電源状態を受信するまで、 **IRP\_MN\_設定\_POWER**の*デバイス*電源の状態。

ある値**Parameters.Power.ShutdownType**保留中の操作に関する追加情報を提供します。 IRP を示す**PowerSystemShutdown** (S5) ドライバーを調べるシステムをリセットするかどうか (**PowerActionShutdownReset**) または後で再起動するには、無期限に電源をオフ (**PowerActionShutdownOff**)。 ほとんどのデバイス ドライバー、違いは重要ではありません。 ただし、デバイス、ストリーミング ビデオなど、特定のデバイス ドライバー可能性があります電源をオフに、デバイス、システムをリセットするときに I/O を停止するには。

Windows 2000 以降のバージョンのオペレーティング システムにある値で**ShutdownType**することもできます**PowerActionShutdown**します。 この場合、ドライバーでは、シャット ダウンの種類が要求され、このためとリセットを実行する必要がありますを見分けることはできません。

**デバイスの電源の状態**

バス ドライバーの上に配置されている関数とフィルター ドライバーでは、デバイスの電源状態を設定する要求は失敗する必要があります。 デバイスが削除された場合、または削除処理中、バス ドライバーは、デバイスの電源を要求にフェールバックできます。

ドライバーは IRP を完了する前に、デバイスが要求された状態に設定する必要があります。

IRP では、低電力状態への遷移を要求するときに、ドライバーはドライバーは、デバイスを動作状態に復元する必要がある任意のコンテキストを保存する、デバイス スタックをたどる際 IRP を処理する必要があります。 バスの後に、ドライバーは、ドライバー、IRP を受信します。

-   ドライバーは、デバイスを動作状態に復元する必要がある任意のコンテキストを保存します。

-   要求された電源の状態、デバイスに設定します。

-   呼び出し[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)電源マネージャーに通知します。

-   呼び出し**PoStartNextPowerIrp** IRP (Windows Server 2003、Windows XP、および Windows 2000 のみ) [次へ] のパワーを開始します。

-   デバイスの電源 IRP を完了します。

ドライバーは、適切なタイミングで、この IRP を完了する必要があります。 一般に、ドライバーは、低下一般的なユーザーを検索する遅延を避ける必要があります。 たとえば、ドライバーでは、キャッシュされたディスクまたはネットワークのデータのフラッシュが必要がありますいないネットワーク接続状態を維持またはテープをフォーマットにシステム状態の変更を遅れる可能性があります。 詳細については、次を参照してください。 [Power Irp を渡して](https://msdn.microsoft.com/library/windows/hardware/ff558785)します。

Windows 2000 以降のバージョンの IRP が指定されている場合、オペレーティング システムで**PowerDeviceD1**、 **PowerDeviceD2**、または**PowerDeviceD3**であり、システム設定 power IRP がアクティブ、ある値**Parameters.Power.ShutdownType** IRP システムに関する情報を提供します。

休止状態パス上のデバイスのドライバーでは、この値を調べる必要があります。 IRP が要求した場合**PowerDeviceD3**と**ShutdownType**は**PowerActionHibernate**、このようなドライバーは、デバイスを復元するために必要な任意のコンテキストを保存する必要がありますが、いない必要がありますデバイスの電源コンピューターの電源が切れたときに、デバイスは D3 の状態を入力します。

Windows 2000 およびそれ以降のバージョンのオペレーティング システムで、ドライバーはある値に依存しない必要があります**ShutdownType**場合、要求された電源の状態が**PowerDeviceD0**します。

Windows 98 で Me IRP がデバイスを要求した場合の電源の状態、/、 **ShutdownType**は常に**PowerActionNone**します。

デバイスの電源するタイミングを決定するドライバーは、デバイス クラスによって異なります。

デバイスの電源をタイミングを決定するドライバーは、ほぼ常に、デバイス レジスタにアクセスするドライバーです。 ドライバーは、登録デバイスのハードウェアにアクセスする前に、デバイスが D0 状態である必要がありますを確認します。 D0 状態で、デバイスがない場合、ドライバーを呼び出す必要があります**PoRequestPowerIrp**デバイスの電源を投入 IRP を送信します。 D0 状態、デバイスがない限り、ドライバーはそのデバイスにアクセスできません。

ドライバーは、D0 のデバイスの状態のセット power IRP を受信するときに、設定、 *IoCompletion*ルーチンを [次へ] の下のドライバーを IRP を渡します。

IRP では、バス ドライバーに達すると、そのドライバーを適用 (またはリセット) 呼び出し、デバイスの電源**PoStartNextPowerIrp** (Windows Server 2003、Windows XP、および Windows 2000 のみ) と呼び出し**PoSetPowerState**新しい電源の状態、デバイスの電源マネージャーに通知します。

関数とフィルター ドライバーの IRP の処理、バス ドライバーには、電源アップ IRP が完了すると、その*IoCompletion*デバイス スタックをバックアップとして、ルーチンが送信されます。 *IoCompletion* 、日常的な各ドライバー復元またはそのデバイス コンテキストを再初期化し、他の必要なスタートアップ タスクを実行します。

詳細については、次を参照してください。 [IRP の処理\_MN\_設定\_デバイスの電源状態のための電力](https://msdn.microsoft.com/library/windows/hardware/ff546885)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff543160)

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IRP\_MN\_クエリ\_電源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)

[**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)

[**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)

[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

[**システム\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff564565)

[**システム\_POWER\_状態\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/jj835780)

 

 




