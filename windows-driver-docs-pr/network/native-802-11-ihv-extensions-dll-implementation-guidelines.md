---
title: ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン
description: ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン
ms.assetid: ef13de2a-3510-46c5-afb6-0bf1002af5ca
keywords:
- IHV Extensions DLL WDK ネイティブ802.11、実装ガイドライン
- ネイティブ 802.11 IHV 拡張 DLL WDK、実装ガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfd96a5f727bf888975d2abf8c04834da27be2f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839644"
---
# <a name="native-80211-ihv-extensions-dll-implementation-guidelines"></a>ネイティブ 802.11 IHV 拡張 DLL 実装ガイドライン




 

IHV 拡張 DLL は、ランタイムダイナミックリンクライブラリ (DLL) として実装されます。 Dll の詳細については、Microsoft Windows SDK のドキュメント内の「ダイナミックリンクライブラリについて」を参照してください。

IHV 拡張 DLL を実装する場合は、次のガイドラインを参照してください。

-   IHV 拡張 DLL によって参照される構造体と関数プロトタイプは、Wlanihv で宣言されます。

-   IHV 拡張 DLL では、 [*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)関数と[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)関数を実装する必要があります。 また、これらの関数は、DLL のビルドに使用されるモジュール定義 (.def) ファイルを使用してエクスポートする必要があります。 オペレーティングシステムは、 **GetProcAddress**関数を使用してこれらの関数のアドレスを解決します。 **GetProcAddress**の詳細については、Windows SDK のドキュメントを参照してください。

-   IHV 拡張 DLL は、すべての IHV ハンドラー関数を実装する必要があります。 オペレーティングシステムが[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)関数を呼び出した場合、DLL はこれらの関数への関数ポインターのリストを返します。

    IHV ハンドラー関数の詳細については、「[ネイティブ 802.11 Ihv ハンドラー関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)」を参照してください。

-   Windows Vista の場合、IHV 拡張 DLL は、インターフェイスのバージョン0をサポートする必要があります。 [*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)が呼び出された場合、DLL では、サポートされるインターフェイスの最小バージョンと最大値を0に定義する必要があります。

 

 





