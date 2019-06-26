---
title: ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン
description: ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン
ms.assetid: ef13de2a-3510-46c5-afb6-0bf1002af5ca
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、実装のガイドライン
- ネイティブ 802.11 IHV 拡張 DLL WDK、実装のガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3e08f32e283e76e5d011843416216485cca470c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387287"
---
# <a name="native-80211-ihv-extensions-dll-implementation-guidelines"></a>ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン




 

IHV 拡張機能の DLL は、実行時のダイナミック リンク ライブラリ (DLL) として実装されます。 Dll の詳細については、」ダイナミック リンク ライブラリの「Microsoft Windows SDK のドキュメント内トピックを参照してください。

IHV の拡張 DLL を実装する場合は、次のガイドラインを参照してください。

-   構造および IHV の拡張機能の DLL によって参照される関数のプロトタイプは、Wlanihv.h で宣言されます。

-   IHV 拡張機能の DLL を実装する必要があります、 [ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)と[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)関数。 また、これらの関数は、DLL をビルドするために使用するモジュール定義 (.def) ファイルをエクスポートする必要があります。 オペレーティング システムは、これらの関数のアドレスを解決、 **GetProcAddress**関数。 詳細については**GetProcAddress**、Windows SDK のマニュアルを参照してください。

-   IHV 拡張機能の DLL には、すべての IHV ハンドラー関数を実装する必要があります。 DLL がオペレーティング システムを呼び出すときに、これらの関数を関数ポインターの一覧を返します、 [ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)関数。

    IHV ハンドラー関数の詳細については、次を参照してください。 [802.11 IHV ハンドラー関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)します。

-   Windows Vista では、IHV 拡張機能の DLL はゼロのインターフェイスのバージョンをサポートする必要があります。 ときに[ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)が呼び出されると、DLL は、最小値を定義する必要がありする最大のサポートされているインターフェイス バージョンは 0。

 

 





