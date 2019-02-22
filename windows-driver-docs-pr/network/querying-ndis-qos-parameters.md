---
title: クエリの NDIS QoS パラメーター
description: クエリの NDIS QoS パラメーター
ms.assetid: 875D39BA-D70D-4450-9F64-D08EAB54BDC2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cbf310d055dd8b48e91d7a204b98be4d472f02c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536332"
---
# <a name="querying-ndis-qos-parameters"></a>クエリの NDIS QoS パラメーター


関連プロトコルとフィルター ドライバーは次の方法でネットワーク アダプターの NDIS サービスの品質 (QoS) パラメーターを照会できます。

-   上にあるドライバーのオブジェクト識別子 (OID) のクエリ要求によって運用上の NDIS QoS パラメーターをクエリできます[OID\_QOS\_運用\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451832)します。

-   上にあるドライバーの OID クエリ要求をリモートの NDIS QoS パラメーターをクエリできます[OID\_QOS\_リモート\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451841)します。

**注**  ドライバーが重なって、ローカルの NDIS QoS パラメーターをクエリできません。

 

ローカル、リモート、および運用上の NDIS QoS パラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](overview-of-ndis-qos-parameters.md)します。

NDIS ミニポート ドライバーのこれらの OID 要求を処理し、内で要求された QoS パラメーターを返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。 NDIS は、次の方法でこれらの OID 要求を処理します。

-   NDIS がの OID のクエリ要求を処理するときに[OID\_QOS\_運用\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451832)から、以前にキャッシュした運用面の NDIS QoS パラメーターを返します[ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)ミニポート ドライバーで発行された状態を示す値。 ドライバーは、運用上の QoS パラメーターが最初に解決されますか、または後で変更するときにこの状態を示す値を発行します。

    上にあるドライバーはドライバーの問題、ミニポートする前に OID クエリ要求を発行する場合、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_の変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状態を示す値、NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)すべてのメンバーを含む構造体 (を除き、 **ヘッダー**メンバー) を 0 に設定します。

    **注**  NDIS は、ミニポート ドライバーの問題がある場合もこの構造体を返します、 [ **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)で状態を示す値を[ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640) (例外でメンバーが構造体**ヘッダー**メンバー) が 0 に設定します。

     

-   NDIS がの OID のクエリ要求を処理するときに[OID\_QOS\_リモート\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451841)から、以前にキャッシュしたリモートの NDIS QoS パラメーターを返します[ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)ミニポート ドライバーで発行された状態を示す値。 ドライバーは、そのリモートの QoS パラメーターが最初に解決されますか、または後で変更するときにこの状態を示す値を発行します。

    上にあるドライバーはドライバーの問題、ミニポートする前に OID クエリ要求を発行する場合、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_の変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態を示す値、NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)すべてのメンバーを含む構造体 (を除き、 **ヘッダー**メンバー) を 0 に設定します。

    **注**  NDIS は、ミニポート ドライバーの問題がある場合もこの構造体を返します、 [ **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)で状態を示す値を[ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640) (例外でメンバーが構造体**ヘッダー**メンバー) が 0 に設定します。

     

 

 





