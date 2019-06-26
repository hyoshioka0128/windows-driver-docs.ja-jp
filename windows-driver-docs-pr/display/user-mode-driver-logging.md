---
title: ユーザー モード ドライバーのログ記録
description: ビデオ メモリのより実用的な内訳を取得するには、Windows Display Driver Model (WDDM) ドライバーはマイクロソフトの Direct3D リソースとビデオ メモリ割り振り間のリレーションシップを公開する必要があります。
ms.assetid: E850E148-821D-4544-A778-00B1B9D13964
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4ebe2158b0299a4d5a29937e0347bb0a9809ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373589"
---
# <a name="span-iddisplayuser-modedriverloggingspanuser-mode-driver-logging"></a><span id="display.user-mode_driver_logging"></span>ユーザー モード ドライバーのログ記録


ビデオ メモリのより実用的な内訳を取得するには、Windows Display Driver Model (WDDM) ドライバーはマイクロソフトの Direct3D リソースとビデオ メモリ割り振り間のリレーションシップを公開する必要があります。 これは、その他のユーザー モード ドライバー (UMD) インターフェイスをログ記録の導入に伴い、Windows 8 以降が可能になります。 この情報を Event Tracing for Windows (ETW) トレースに追加するは、API の観点から、ビデオ メモリの割り当てを表示できます。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| WDDM の最小バージョン                                                              | 1.2                              |
| Windows の最小バージョン                                                           | 8                                |
| ドライバーの実装: 完全なグラフィックスとレンダリングのみ                               | 必須                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | **Device.Graphics¦UMDLogging** |

 

開発者は、UMD ログ記録が現在内部断片化やサーフェスを迅速に破棄の影響などを表示する非常に困難なメモリのコストを明確にできます。 Microsoft は、お客様とパートナー様のパフォーマンスの問題の分析トレースを提供の向上に使用することできます。 具体的には、この機能が、メモリに関連するパフォーマンスの問題の調査に一般的なブロッキングのポイントを克服するために役立ちます。: アプリケーションは、大きすぎてのワーキング セットを使用して、API リソースを決定することはできませんが、または呼び出しは、問題を引き起こしています。

ドライバーは、UMD ETW インターフェイスを実装する Direct3D リソースとビデオ メモリ割り振り間のリレーションシップを公開する必要があります。 ドライバーは、だけでなく、ログ記録イベントのリソースと任意の時点の割り当てのすべての既存のマッピングを報告できる必要があります。

## <a name="span-idumddriverallocationloggingddispanspan-idumddriverallocationloggingddispanspan-idumddriverallocationloggingddispanumd-driver-allocation-logging-ddi"></a><span id="UMD_driver_allocation_logging_DDI"></span><span id="umd_driver_allocation_logging_ddi"></span><span id="UMD_DRIVER_ALLOCATION_LOGGING_DDI"></span>ログ DDI UMD ドライバーの割り当て


ユーザー モード ドライバーの割り当てのログ記録のデバイス ドライバー インターフェイス (DDI) は、API リソースは、Microsoft DirectX では、どのカーネル割り当てに関連付けられたかを示す、Event Tracing for Windows (ETW) のカーネル レベルのトレース機能の下のイベントを提供します。グラフィックスのカーネル サブシステム (Dxgkrnl.sys) です。

DDI を使用するには、内部メモリの断片化またはサーフェスを迅速に破棄されるの影響を見つけ、パフォーマンスの問題を特定して、アプリのリソースまたは API を呼び出すと判断するための Microsoft のより詳細なトレース情報を提供するには原因となって、大きすぎてのワーキング セットのメモリを使用するようにします。

これらの関数を使用して、ディスプレイ ドライバーの列挙、およびユーザー モードでイベントを記録する Umdprovider.h ヘッダーからの構造体。

-   [**UMDEtwLogMapAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/nf-umdprovider-umdetwlogmapallocation)関数
-   [**UMDEtwLogUnmapAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/nf-umdprovider-umdetwlogunmapallocation)関数
-   [**UMDEtwRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/nf-umdprovider-umdetwregister)関数
-   [**UMDEtwUnregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/nf-umdprovider-umdetwunregister)関数
-   [**UMDETW\_割り当て\_SEMANTIC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/ne-umdprovider-_umdetw_allocation_semantic)列挙型
-   [**UMDETW\_割り当て\_使用状況**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/umdprovider/ns-umdprovider-_umdetw_allocation_usage)構造体

また、Umdetw.h ヘッダーを参照してください。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... UMDLogging**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





