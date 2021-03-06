---
title: WHEA が ECC メモリ上で PFA を実行する方法
description: WHEA が ECC メモリ上で PFA を実行する方法
ms.assetid: def94688-9ca6-4146-8d5b-4c3550d3d272
keywords:
- 予測的な失敗の分析 (PFA) WDK WHEA、エラー訂正コードのメモリ
- PFA WDK WHEA、エラー訂正コードのメモリ
- エラー訂正コード メモリ WDK WHEA
- エラー訂正コード メモリ WDK WHEA、予測的な失敗の分析
- 低レベル ハードウェア エラー ハンドラー WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08386323a75e6991fc0e81a20d442cd8b18f9bdb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386471"
---
# <a name="how-whea-performs-pfa-on-ecc-memory"></a>WHEA が ECC メモリ上で PFA を実行する方法


Windows 7 以降、Windows ハードウェア エラー アーキテクチャ (WHEA) は、エラー修正コード (ECC) メモリの予測的な障害の分析 (PFA) をサポートします。

WHEA は、次の条件に当てはまる場合にのみ、ECC メモリ ページに対して PFA を実行します。

-   レジストリ値**MemPfaDisable** 1 に設定されていません。

-   A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)が既に設定されていない、 **PlatformPfaControl**ビット、 [ **WHEA\_エラー\_パケット\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_flags)のメンバー、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造体を 1 にします。 プラグインに設定 PFA を実行する場合のこのビットをします。 PFA の実行方法でこのプラグインの詳細については、次を参照してください。 [PFA 実行プラグイン PSHED](pfa-performed-by-a-pshed-plug-in.md)します。

[メモリ] ページは、ECC メモリ エラーが発生するときに WHEA は、次の手順に従って ECC メモリ ページで PFA を実行します。

1.  WHEA ECC メモリ ページがいない監視は現在場合、WHEA はページの監視のデータベースに追加し、エラーの数と、新しいエントリのティック数をクリアします。

    **注**WHEA はティック数を超えたとき、ECC メモリ ページの監視を停止、 **MemPfaTimeout**レジストリ値。 この場合、WHEA の監視のデータベースからエントリを削除します。



2.  WHEA では、ECC メモリ ページのエラー数をインクリメントします。

3.  エラーの数を超えた場合、 **MemPfaThreshold**レジストリ値、WHEA 最初、システム メモリ マネージャーを呼び出し、ECC メモリ ページをオフラインにします。

    **注**システムのメモリ マネージャーが呼び出されたときに、ECC メモリ ページが実際にオフラインされる保証はありません。




WHEA では、システム ストアでのブート構成データ (BCD) に、メモリ ページが、追加します。 これは、メモリ ページが次のシステム再起動後に使用されていることを防ぎます。

**注**WHEA になります、ECC メモリ ページなどのハードウェア コンポーネント オフライン場合、レジストリ値**DisableOffline** 0 以外の値に設定されています。 また、WHEA に追加されません、ECC メモリ ページ、BCD ストア場合、レジストリ値**MemPersistOffline** 0 に設定されます。




WHEA の PFA レジストリ値に関する詳細については、次を参照してください。 [WHEA ポリシー設定](whea-pfa-registry-settings.md)します。

システムのメモリ マネージャーの詳細については、次を参照してください。、[メモリ管理](https://go.microsoft.com/fwlink/p/?linkid=140723)Windows SDK のドキュメント。








