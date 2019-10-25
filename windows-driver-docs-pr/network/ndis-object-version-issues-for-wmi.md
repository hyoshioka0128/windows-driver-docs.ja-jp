---
title: WMI の NDIS オブジェクト バージョンの問題
description: WMI の NDIS オブジェクト バージョンの問題
ms.assetid: 09440de8-125b-4155-9f28-c9f6893071b2
keywords:
- NDIS バージョン情報 WDK、WMI サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff635f89567863fb15c0a6fd2929aee468a56ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844363"
---
# <a name="ndis-object-version-issues-for-wmi"></a>WMI の NDIS オブジェクト バージョンの問題





このトピックでは、Windows Management Instrumentation (WMI) のサポートに影響する NDIS オブジェクトバージョンの問題について説明します。

WMI 管理オブジェクトフォーマット (MOF) ファイル内にバージョン管理はありません。 したがって、対応する NDIS 構造に新しいリビジョンがある場合は、MOF データオブジェクトにさらに多くのフィールドが追加されています。

新しいバージョンの NDIS に追加メンバーが追加されると、NDIS\_WMI\_Xxx\_ヘッダー構造に新しいリビジョンが追加されます。 現在の NDIS\_WMI\_Xxx\_ヘッダー構造の一覧については、「 [NDIS WMI 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)」を参照してください。

アプリケーションがクエリ操作の WMI 情報にアクセスするときは、データにアクセスする前に、返されたバッファーのバージョンを確認する必要があります。 設定操作の場合、アプリケーションは、NDIS\_WMI\_OUTPUT\_INFO 構造体の**Supportedrevision**メンバーを調べて、基になるドライバーが受け入れたバージョンを特定する必要があります。

多くの WMI オブジェクトには、 **MSNdis\_ObjectHeader**プロパティが含まれています。これは、 [**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)構造に相当します。 **MSNdis\_ObjectHeader**プロパティを設定するときに、「 **NDIS\_オブジェクト\_ヘッダー** 」に記載されているように、 **Type**フィールドと**Revision**フィールドを設定します。 64ビットシステムへのシームレスな移植性を確保するには、 **Size**フィールドを `0xFFFF`に設定します。

## <a name="related-topics"></a>関連トピック


[NDIS バージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報の指定](specifying-ndis-version-information.md)

 

 






