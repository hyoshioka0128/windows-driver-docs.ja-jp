---
title: 暗号化のサポート
description: 暗号化のサポート
ms.assetid: d5ce9c02-7126-4775-bb87-dae45b93b652
keywords:
- ビデオデコード WDK DirectX VA、暗号化
- ビデオをデコードする WDK DirectX VA、暗号化
- 画像デコード WDK DirectX VA、暗号化
- 暗号化 WDK DirectX VA
- 暗号化 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe5243f7c23db8ab9a16b914be54faa2f4bd77e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838951"
---
# <a name="encryption-support"></a>暗号化のサポート


## <span id="ddk_encryption_support_gg"></span><span id="DDK_ENCRYPTION_SUPPORT_GG"></span>


ビデオのデコードに使用されるデータは、次の構造とデータ型に対して暗号化できます。

-   マクロブロックコントロールコマンドの構造

-   残余差ブロック構造体

-   ビットストリームバッファー

ホストデコーダーが暗号化を使用するためには、アクセラレータがサポートする暗号化の種類を決定する必要があります。 アクセラレータによってサポートされる暗号化の種類に関する情報は、ビデオアクセラレータ形式の Guid としてホストに提供される暗号化の種類の Guid の一覧に含まれています。 ビデオアクセラレータ形式 Guid の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

すべての DirectX VA アクセラレータは、暗号化を使用せずに動作できる必要がある**ことに注意**してください  。 このため、暗号化を使用しないでの操作はサポートされていないため、を宣言する必要はありません。また、DXVA\_NoEncrypt "no encryption" GUID を video accelerator format GUID リストで送信することはできません。

 

ホストは、適用する暗号化プロトコルの種類を選択し、アクセラレータに GUID を送信することでこの選択を示します。 一般的な暗号化のシナリオでは、暗号化されたデータを正常に転送する前に、次の2つの手順を実行します。

1.  ホストデコーダーでは、データを受信する権限がアクセラレータに付与されていることを確認する必要があります。 この検証を行うには、アクセラレータを使用して署名された構造体をホストに渡して、承認された公開/秘密キーのペアを保持していることを証明します。

2.  次に、ホストデコーダーは、暗号化されたコンテンツキーをアクセラレータに送信します。

暗号化プロトコルを初期化する手順の正確な数は、使用する暗号化の種類と実装方法によって異なります。

必要な暗号化初期化パラメーターを渡すために、ホストとアクセラレータの間で交換される各データセットには、暗号化プロトコルの種類の GUID がプレフィックスとして付けられている必要があります。 この GUID は、ある種類の暗号化のデータを別の種類のデータと区別します。 これは、1つの DirectX VA バッファーに対して1種類の暗号化を使用し、別の種類の暗号化を別の DirectX VA バッファーに使用できるために必要です。

[**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)構造体は、暗号化プロトコルが使用されていること、および使用されている暗号化の種類を示すために使用されます。

 

 





