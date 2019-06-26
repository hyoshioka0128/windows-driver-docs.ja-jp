---
title: 同じハードウェア上の複数のデータ ストリーム
description: 同じハードウェア上の複数のデータ ストリーム
ms.assetid: 23133022-6d00-44ad-8c0d-24715204cacc
keywords:
- 複数のデータ ストリームの WDK DVD デコーダー
- ストリームの番号には、WDK DVD デコーダーがサポートされています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a677d867fc828438dbc0c7c9cb58b396156927e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363282"
---
# <a name="multiple-data-streams-on-the-same-hardware"></a>同じハードウェア上の複数のデータ ストリーム





多くのデコーダーでは、デコーダーのハードウェアの同じ部分を使用して複数のストリームがあります。 これらのデバイスでは、各ストリームでキーのネゴシエーションを個別に実行する必要はありません。 DVD デコーダーのモデルには、これを示すを使用して、 [ **KS\_DVDCOPY\_設定\_コピー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)プロパティ。 このプロパティの get 操作が発行されると、デコーダーが、次のいずれかの応答します。

KS\_DVDCOPYSTATE\_認証\_いない\_必要な作業

KS\_DVDCOPYSTATE\_認証\_必要な作業

KS\_DVDCOPYSTATE\_認証\_いない\_必要な作業は、指定したストリームが必要としないことキーのネゴシエーション、同じハードウェア上の別のストリームが実行して既にためにことを示します。 例では、デコーダーが受信した場合、**取得**プロパティ オーディオのストリームで最初に、応答した**KS\_DVDCOPYSTATE\_認証\_REQUIRED**でオーディオ ストリームと**KS\_DVDCOPYSTATE\_認証\_いない\_REQUIRED**他のすべてのストリームにします。 認証の応答の後\_いない\_必要に応じて、そのストリームを受け取りません以上のキーの交換プロパティまで、[次へ] のタイトルのキーがネゴシエートされます。 その時点では、デコーダーは、認証で返信する選択可能性がありますもう一度\_いない\_必要な作業です。

DVD の再生、デコーダーが 1 つだけストリームを著作権保護を実行する必要がある場合以外は、その他のアプリケーションでは、デコーダーでは、受信する最初のストリームのネゴシエーションを実行する**取得**のプロパティの呼び出し**KS\_DVDCOPY\_設定\_コピー\_状態**ストリームの開始後にします。 1 つのみのストリームを使用する著作権保護のプロパティをハードコーディングしないでください。

 

 




