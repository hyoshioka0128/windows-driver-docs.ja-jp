---
title: LE ハング検出
description: このセクションには、WDI に LE ハング検出がについて説明します
ms.assetid: 9C0BB4B8-184A-4C1A-8B47-C30C8318AEEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 966b6d52548c937c3479bab0af8736e855ad6950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551044"
---
# <a name="le-hang-detection"></a>LE ハング検出


一部のファームウェアでは、ファームウェアのハングを検出できるウォッチドッグ タイマーがあります。 一部の IHV ドライバー (LE) では、ファームウェアによって進行が行われていないかどうかを検出するロジックがあります。 UE は、このような状況を示す LE を使用できます。

アダプターのポートでの表示をする必要があります (たとえば、ポート id = 0 xffff)。 既定では、指標が手順を実行する、完全なリセット recovery--LE をトリガー呼び出しの診断、情報、および要求側 PLDR デバッグを収集します。

LE またはファームウェアのウォッチドッグ タイマーは、ファームウェアの停滞を検出すると、UE から期待次に示します。

1.  D0 の場合
    1.  LE を示します[NDIS\_状態\_WDI\_INDICATION\_ファームウェア\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)します。
    2.  表示から戻り値に、LE を返します (存在する場合)、ストールした WDI コマンド。
    3.  UE は、回復のリセット (RR) プロシージャを開始します。

2.  Dx の場合これはのみ検出ファームウェア失速で発生します。
    1.  ファームウェアは、ウェイク アップの割り込みを発生させます。
    2.  D0 コマンドを受信するには、理由、ファームウェアの一時停止などのウェイク アップの理由を示します。
    3.  D0 WDI OID を返された後、LE ことを示します[NDIS\_状態\_WDI\_INDICATION\_ファームウェア\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)します。
    4.  D0 と手順を完了するには。1a、1b、および 1 c。

![wdi le ハング検出](images/wdi-le-hang-detection-flow.png)

## <a name="hang-detection-in-dx"></a>ハング Dx の検出


ファームウェアが Dx で進行状況が停止することができます。 ここでは、Dx は PCIe NIC の D3Hot と USB と SDIO D2 です。 NIC wake を入手できますと自律的に、アクセス ポイントの関連性を維持または NLO のスキャンが必要です。 ない場合は関連付けられています。

NIC は、Dx では、電源オフ状態である可能性がバスのためホストへの通信がブロックされます。 したがって、LE は停止しているファームウェアを検出することではありません。 ファームウェア自体は、条件を検出し、D0、ACPI または bus 完了を通じて間接的にスタックを持ち込むウェイク行 (コードのスリープ解除部分がアライブの場合) を生成する必要があります、NDIS 待機\_wake\_irp します。 このため、NDIS は、NIC に D0 を設定します。

ファームウェアでは、このような条件をウェイク アップをアサートします。 LE、ファームウェアのウェイク アップの理由を示す必要があります。 ウェイク アップの理由**WDI\_WAKE\_理由\_コード\_ファームウェア\_STALLED**ウェイク アップの理由である列挙型として定義されます。

Recovery にこのシナリオで動作する、リセット、ファームウェアの少なくとも 2 つの部分はまだ動作する必要があります。

1.  ハング検出コード。
2.  ウェイク アップの割り込みをアサートするコードです。

いずれかが不足している場合は、ホスト側がファームウェアが停止し、RR は発生しないかどうかは認識しません。 このシナリオは、設計の目標の一部ではありません。

![wdi hang detection in dx](images/wdi-hang-detection-dx.png)

## <a name="os-module-triggered-reset-recovery"></a>トリガーされた OS モジュールは、復旧をリセット


これは、ihv 向けの情報です。 他に、UE と LE にハングが検出された場合、その他の OS コンポーネントがハングを検出またはリセット Recovery プロシージャを呼び出す UE をトリガーすることがあります。 現時点では、Windows 10 では、ユーザー モード wlansvc コンポーネントは、インターネットと接続の接続を検出し、その後しばらくの間の関連付けを解除せず、DNS サーバーにアクセスする機能を失うときに、UE へのリセットの回復を要求できます。 今後、Microsoft には、エンドユーザーを強化するためにリセット復旧が発生したトリガーに追加のケースがあります。

## <a name="related-topics"></a>関連トピック


[NDIS\_状態\_WDI\_INDICATION\_ファームウェア\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)

[**WDI\_TLV\_INDICATION\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/dn897834)

 

 






