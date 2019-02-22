---
title: NDIS プロトコル ドライバーから OID 要求を生成します。
description: NDIS プロトコル ドライバーから OID 要求を生成します。
ms.assetid: a27d1c9c-fc7e-414f-8cad-595e8d8fe8f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba05cb659bf9ae9ec87b28112152974e81fa22fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549253"
---
# <a name="generating-oid-requests-from-an-ndis-protocol-driver"></a>NDIS プロトコル ドライバーから OID 要求を生成します。





プロトコルの呼び出しを基になるドライバーの OID 要求を発信、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)関数。

次の図は、プロトコル ドライバーによって送信されたが、OID 要求を示しています。

![プロトコル ドライバーで発生した、oid 要求を示す図](images/protocolrequest.png)

プロトコル ドライバーを呼び出してから、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)関数、NDIS は、[次へ] の基になるドライバーの要求関数を呼び出します。 ミニポート ドライバーが OID 要求を処理する方法の詳細については、次を参照してください。[アダプターの OID 要求](miniport-adapter-oid-requests.md)します。 フィルター ドライバーが OID 要求を処理する方法の詳細については、次を参照してください。[フィルター モジュールの OID 要求](filter-module-oid-requests.md)します。

同期的に完了する**NdisOidRequest**返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する**NdisOidRequest**返します NDIS\_状態\_保留します。

場合**NdisOidRequest**返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570264)関数の後に、基になるドライバーでは、OID 要求を完了します。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolOidRequestComplete*します。

場合**NdisOidRequest** NDIS を返します\_状態\_成功するでのクエリ要求の結果が返されますが、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)で構造体、 *OidRequest*パラメーター。 この場合は、NDIS は呼び出しません、 *ProtocolOidRequestComplete*関数。

どのような情報が正常に処理によって基になるドライバーでは、OID を発行するプロトコル ドライバーを決定する要求は、値を確認する必要があります、 **SupportedRevision** NDIS でメンバー\_OID\_要求OID 要求が返された後に構造体。 NDIS バージョン情報の詳細については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

場合は、基になるドライバーは、それ以降の状態を示す値を OID 要求を関連付ける必要があります、プロトコル ドライバーに設定する必要があります、 **RequestId** NDIS でメンバー\_OID\_要求の構造。 基になるドライバーは、状態の表示を行うときに、設定、 **RequestId**内のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体OID で指定された値を次のように要求します。

ドライバーを呼び出すことができます**NdisOidRequest**でバインディングの場合、*再起動*、*を実行している*、*一時停止中*、または*を一時停止*状態。

 

 





