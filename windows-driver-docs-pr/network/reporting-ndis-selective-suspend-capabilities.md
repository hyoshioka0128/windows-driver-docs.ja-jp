---
title: NDIS セレクティブ サスペンド機能のレポート
description: NDIS セレクティブ サスペンド機能のレポート
ms.assetid: 8A738A51-D116-4DDC-96B7-17D046B6890D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef06c17c209901206be6b774281311ef6fbb448
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574683"
---
# <a name="reporting-ndis-selective-suspend-capabilities"></a>NDIS セレクティブ サスペンド機能のレポート


NDIS 6.30 のミニポート ドライバーを開始する必要がありますレポート、ドライバーが選択的 NDIS のサポートを有効にするかどうかを中断します。 サポートの NDIS 選択的な中断が有効かの設定を無効になっている、  **\*SelectiveSuspend** INF キーワードを標準化します。 この INF キーワードの詳細については、次を参照してください。 [NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)します。

NDIS がドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数、ミニポート ドライバーは、次の手順で選択的 NDIS サスペンドのサポートをそのサポートを報告します。

1.  ドライバーの初期化、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)基になるハードウェアの電源管理機能を含む構造体。

    メンバーを設定する必要があります、ドライバーのサポートを有効 NDIS 選択的な中断する場合、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)次のように構造体します。

    -   NDIS ミニポート ドライバーを指定してください\_PM\_機能\_リビジョン\_2 および NDIS\_SIZEOF\_NDIS\_PM\_機能\_リビジョン\_リビジョンと長さの 2、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)の構造体の内部構造**ヘッダー**メンバー。
    -   場合、  **\*SelectiveSuspend**キーワードのいずれかの値は、NDIS 選択的な中断のミニポート ドライバーのサポートは有効です。 ミニポート ドライバーを報告するには、NDIS\_PM\_セレクティブ\_SUSPEND\_内でサポートされているフラグ、**フラグ**この構造体のメンバー。

2.  これが初期化されると、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体、ミニポート ドライバーのセット、 **PowerManagementCapabilitiesEx**メンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)初期化を指す構造体**NDIS\_PM\_機能**構造体。 ミニポート ドライバーへのポインターを渡す、 **NDIS\_ミニポート\_アダプター\_全般\_属性**構造体、 *MiniportAttributes*ドライバーを呼び出すと、パラメーター、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

レポートの選択的 NDIS のサポート状況サスペンドするミニポート ドライバーで使用されるメソッドは、電源管理機能を報告するための NDIS 6.20 が動作方法に基づきます。 この方法の詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

 

 





