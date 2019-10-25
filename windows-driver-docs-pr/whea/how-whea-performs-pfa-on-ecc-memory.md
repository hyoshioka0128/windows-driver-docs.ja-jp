---
title: WHEA が ECC メモリ上で PFA を実行する方法
description: WHEA が ECC メモリ上で PFA を実行する方法
ms.assetid: def94688-9ca6-4146-8d5b-4c3550d3d272
keywords:
- 予測エラー分析 (PFA) WDK WHEA、エラー修正コードメモリ
- PFA WDK WHEA、エラー修正コードのメモリ
- エラー修正コードメモリ WDK WHEA
- エラー修正コードメモリ WDK WHEA、予測エラー分析
- 低レベルのハードウェアエラーハンドラー WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d9cbed229c7dd2f2e677d2c24b4f5b90777983
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844401"
---
# <a name="how-whea-performs-pfa-on-ecc-memory"></a>WHEA が ECC メモリ上で PFA を実行する方法


Windows 7 以降では、Windows ハードウェアエラーアーキテクチャ (WHEA) は、エラー修正コード (ECC) メモリの予測エラー分析 (PFA) をサポートしています。

WHEA は、次の条件に当てはまる場合にのみ、ECC メモリページで PFA を実行します。

-   レジストリ値**Mempfadisable**が1に設定されていません。

-   [プラットフォーム固有のハードウェアエラードライバー (pshed) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)は、以前は\_Whea のビットを設定していませんでした。この[**エラー\_パケット\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)のメンバーである[whea\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造体を1にします。 プラグインは、PFA を実行している場合、このビットを設定します。 このプラグインによる PFA の実行方法の詳細については、「 [Pfa プラグインによって実行される pfa](pfa-performed-by-a-pshed-plug-in.md)」を参照してください。

メモリページで ECC メモリエラーが発生した場合、WHEA は次の手順に従って [ECC メモリ] ページで PFA を実行します。

1.  WHEA が現在 ECC メモリページを監視していない場合、WHEA はページを監視データベースに追加し、新しいエントリのエラー数とティック数をクリアします。

    **メモ** のティックカウントが**MemPfaTimeout**レジストリ値を超えた場合、WHEA は [ECC メモリ] ページの監視を停止します。 この場合、WHEA は監視データベースからエントリを削除します。



2.  WHEA は、[ECC メモリ] ページのエラー数を増やします。

3.  エラー数が**Mempfathreshold**レジストリ値を超えた場合、WHEA はまずシステムメモリマネージャーを呼び出して、ECC メモリページをオフラインにします。

    **メモ** システムメモリマネージャーを呼び出すと、ECC メモリページが実際にオフラインになるという保証はありません。




次に、WHEA は、メモリページをシステムストアのブート構成データ (BCD) に追加します。 これにより、次回のシステム再起動後にメモリページが使用されなくなります。

**メモ** レジストリ値**Disableoffline**が0以外の値に設定されている場合、WHEA は、ECC メモリページなどのハードウェアコンポーネントをオフラインにしません。 また、レジストリ値**Mempersistoffline**が0に設定されている場合、WHEA は BCD ストアに ECC メモリページを追加しません。




WHEA の PFA レジストリ値の詳細については、「 [Whea ポリシー設定](whea-pfa-registry-settings.md)」を参照してください。

システムメモリマネージャーの詳細については、Windows SDK のドキュメントの「[メモリ管理](https://go.microsoft.com/fwlink/p/?linkid=140723)」を参照してください。








