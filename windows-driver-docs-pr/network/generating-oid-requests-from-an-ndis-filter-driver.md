---
title: NDIS フィルター ドライバーから OID 要求を生成します。
description: NDIS フィルター ドライバーから OID 要求を生成します。
ms.assetid: 6567bf98-bf56-4337-8670-af4c78d2c947
keywords:
- Oid WDK ネットワー キング、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a42b1496e4539e05477b333be2bf9a3cb7b2894
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549585"
---
# <a name="generating-oid-requests-from-an-ndis-filter-driver"></a>NDIS フィルター ドライバーから OID 要求を生成します。





フィルター ドライバーを OID のクエリを生成または呼び出すことによって、基になるドライバーに要求を設定、 [ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)関数。

次の図は、フィルター ドライバーで発生した OID 要求を示しています。

![フィルター ドライバーで発生した、oid 要求を示す図](images/filterrequest.png)

フィルター ドライバーを呼び出してから、 [ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)関数、NDIS は、[次へ] の基になるドライバーの要求関数を呼び出します。 ミニポート ドライバーが OID 要求を処理する方法の詳細については、[アダプターの OID 要求](miniport-adapter-oid-requests.md)を参照してください。

同期的に完了する[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する**NdisFOidRequest**返します NDIS\_状態\_保留します。

どのような情報が正常に処理を基になるドライバーでは、OID を発行するフィルター ドライバーを決定する要求は、値を確認する必要があります、 **SupportedRevision** NDIS でメンバー\_OID\_要求OID 要求が返された後に構造体。 NDIS バージョン情報の詳細については、[NDIS バージョン情報を指定する](specifying-ndis-version-information.md)を参照してください。

場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)基になるドライバー OID 要求の完了後も機能します。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*FilterOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*FilterOidRequestComplete*します。

場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返します NDIS\_状態\_成功すると、クエリ要求の結果を[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)で構造体、 *OidRequest*パラメーター。 この場合は、NDIS は呼び出しません、 [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)関数。

ドライバーを呼び出すことができます[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)内にある場合、*再起動*、*を実行している*、*一時停止中*、または*Paused*状態。

**注**  フィルター ドライバーが発生する OID 要求の追跡し、呼び出されないことを確認する必要があります、 [ **NdisFOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561833)関数とそのような要求が完了します。

 

 

 





