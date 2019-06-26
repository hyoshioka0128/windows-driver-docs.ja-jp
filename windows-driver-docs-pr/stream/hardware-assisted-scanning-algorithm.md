---
title: ハードウェア補助スキャン アルゴリズム
description: ハードウェア補助スキャン アルゴリズム
ms.assetid: 9a24b985-9667-4424-84e5-b1c728b3c558
keywords:
- ハードウェアによる WDK ビデオ キャプチャのスキャン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c99aaabcc3f8b327b62eced37328400e160ebec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384015"
---
# <a name="hardware-assisted-scanning-algorithm"></a>ハードウェア補助スキャン アルゴリズム


**このセクションでは、Microsoft Windows Vista 以降のオペレーティング システムにのみ適用されます。**

ドライバーの設定、 **fSupportsHardwareAssistedScanning**のメンバー、 [ **KSPROPERTY\_チューナー\_スキャン\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)構造体への呼び出しでその[ **KSPROPERTY\_チューナー\_スキャン\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps)をその it とその関連するハードウェアを示すプロパティイベント ベースのスキャン操作をサポートします。 チューナー フィルター (*KsTvTune.ax*) ドライバーの KSPROPERTY を呼び出す\_チューナー\_スキャン\_CAPS プロパティをドライバーがハードウェア依存のスキャンをサポートしているかどうかを判断します。 チューナー フィルターの呼び出しも、KSPROPERTY\_チューナー\_スキャン\_ブロードキャストを決定する上限ネットワーク ドライバーがスキャンをサポートする型。 かどうか、ドライバーは、ハードウェア依存のスキャンがサポートを返すことができますスキャン機能では、各ブロードキャスト ネットワークがサポートされている型の[ **KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps)プロパティ。 例については、容量の設定が安定する頻度のチューニングのデバイスが必要な時間の指定 (うちは落ち着かない時間) のスキャン機能が含まれてし、チューニングのフィルターが、調整可能なの存在を感知を使用して、周波数の範囲を提供します。(範囲を検知) 信号。 アナログのブロードキャスト ネットワークの機能をスキャンする方法については、次を参照してください。、 [**チューナー\_アナログ\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tuner_analog_caps_s)構造体。

*KsTvTune.ax*概算値として解決時間の値を使用します。 *KsTvTune.ax*周波数の範囲をスキャンし、検出範囲に基づく、スキャン プロセスにどのくらいの時間がかかる閉じる推定値を持つアプリケーションを提供することができます。 ドライバーの後に[ **KSEVENT\_チューナー\_開始\_スキャン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)スキャン プロセスを開始するイベントが呼び出される、アプリケーションはイベントを待つことができます規定の時間を通知します。

ドライバーはどちらのチューナーを返しますにシグナルをチューニングのデバイスがロックされているかどうかに応じて、ハードウェアによるスキャンの\_LockType\_None またはチューナー\_LockType\_そのへの呼び出しからのステータスがロックされています。[**KSPROPERTY\_チューナー\_スキャン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)プロパティ。 シグナルにドライバーがロックされている場合、ドライバーはロックされている信号の頻度も返します。

 

 




