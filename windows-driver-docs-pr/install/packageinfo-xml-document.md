---
title: PackageInfo XML ドキュメント
description: PackageInfo XML ドキュメント
ms.assetid: 1fa9b8a5-d6ab-4952-8e2d-7cb7ccc88804
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 116aaffd2285ba77ea63681326967f5aefdac94e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365826"
---
# <a name="packageinfo-xml-document"></a>PackageInfo XML ドキュメント


PackageInfo の XML ドキュメントには、デバイス メタデータ パッケージの内容を指定するデータが含まれています。 オペレーティング システムでは、このデータを使用するパッケージをインストールし、その内容を参照します。

デバイス メタデータ システムのコンポーネントなど、 [Windows メタデータとインターネット サービス](windows-metadata-and-internet-services.md)(WMIS) と[デバイス メタデータの取得クライアント](device-metadata-retrieval-client.md)(DMRC) を提供する PackageInfo XML ドキュメントを使用して、デバイスとプリンター デバイスの場合、次のよう最新かつ最も適切な情報をユーザー インターフェイス:

-   デバイスのハードウェアまたはモデルの ID。 この情報がで指定された、 [ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))と[ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) PackageInfo XML ドキュメント内の XML 要素。

-   コンピューターのロケールに一致するデバイス メタデータ パッケージのローカライズ版。 この情報がで指定された、 [**ロケール**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548647(v=vs.85)) PackageInfo XML ドキュメント内の XML 要素。

-   最後は、コンピューターのロケールに一致するデバイス メタデータ パッケージのデータを変更します。 この情報がで指定された、 [ **LastModifiedDate** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) PackageInfo XML ドキュメント内の XML 要素。

各デバイス メタデータ パッケージは、1 つだけの PackageInfo XML ドキュメントを含める必要があります。 ドキュメントの名前である必要があります*PackageInfo.xml*します。

PackageInfo の XML ドキュメント内のデータはに基づいて書式設定、 [PackageInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))します。

 

 





