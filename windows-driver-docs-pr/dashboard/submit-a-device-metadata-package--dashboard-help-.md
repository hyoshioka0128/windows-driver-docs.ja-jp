---
title: デバイス メタデータ パッケージの提出 (ダッシュボード ヘルプ)
description: デバイス メタデータ パッケージの提出 (ダッシュボード ヘルプ)
ms.assetid: dcd35784-51c3-410a-8704-94f07fa8959a
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f220bc220e5d7b750868e776f68fec313f0855
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334913"
---
# <a name="submit-a-device-metadata-package-dashboard-help"></a>デバイス メタデータ パッケージの提出 (ダッシュボード ヘルプ)


新しいデバイス メタデータ パッケージを作成した後、または既にあるパッケージを置き換えた後は、検証とその後の発行の対象となるパッケージを提出できます。

## <a name="span-idsubmittingadevicemetadatapackagespanspan-idsubmittingadevicemetadatapackagespanspan-idsubmittingadevicemetadatapackagespansubmitting-a-device-metadata-package"></a><span id="Submitting_a_device_metadata_package"></span><span id="submitting_a_device_metadata_package"></span><span id="SUBMITTING_A_DEVICE_METADATA_PACKAGE"></span>デバイス メタデータ パッケージの申請


同じ方法を使って、パッケージをプレビュー用またはリリース用に提出できます。

**デバイス メタデータ パッケージを申請するには**

1.  [SignTool ツール](https://go.microsoft.com/fwlink/p/?LinkId=238330)を使って、メタデータ パッケージに署名します。

2.  ハードウェア デベロッパー センターまたは Windows デベロッパー センターから Microsoft アカウントで**ダッシュボード**にサインインします。

3.  **[Device metadata]** (デバイス メタデータ) で、 **[Create experience]** (エクスペリエンスの作成) (新しいエクスペリエンスを提出する場合)、または **[Manage experience]** (エクスペリエンスの管理) (既にあるエクスペリエンスを変更する場合) をクリックします。

4.  新しいエクスペリエンスを参照して選び、 **[Submit]** (送信) をクリックします。

詳しくは、「[デバイス メタデータ エクスペリエンスの作成](https://msdn.microsoft.com/library/windows/hardware/br230794.aspx)」または「[デバイス メタデータ エクスペリエンスの管理](https://msdn.microsoft.com/library/windows/hardware/br230797.aspx)」をご覧ください。

提出プロセスの間、ダッシュボードによってエクスペリエンスのパッケージが検証されます。

### <a name="span-idpackagevalidationspanspan-idpackagevalidationspanspan-idpackagevalidationspanpackage-validation"></a><span id="Package_validation"></span><span id="package_validation"></span><span id="PACKAGE_VALIDATION"></span>パッケージの検証

申請中、ダッシュボードは、それぞれのパッケージに対して次の操作を実行します。

-   ファイルがコード署名されていることを確かめる。

-   ウイルス スキャンを実行する。

-   パッケージの構造を調べる。

-   適切なスキーマに対してすべての .xml ファイルを検証する。

-   すべてのアイコンが指定の Windows オペレーティング システムに準拠していることを確かめる。

-   .xml ファイルのすべてのリレーショナル フィールドが既にあるリソースをポイントしていることを確かめる。

-   すべての必要なタスクとステータス要素が DeviceStage パッケージに含まれていることを確かめる。

-   デバイス エクスペリエンスに結び付けられたハードウェア認定提出が、適切なデバイスを対象としていることを確かめる。

-   日付値をパッケージに書き込み、デバイス エクスペリエンスを確かめる。

-   それぞれのディレクトリに検証を示す .cat ファイルを作成し、署名する。

-   パッケージを再構成し、GUID として名前を変更する。

-   デバイス メタデータ パッケージに署名する。

### <a name="span-idsubmittingaservicemetadatapackagespanspan-idsubmittingaservicemetadatapackagespanspan-idsubmittingaservicemetadatapackagespansubmitting-a-service-metadata-package"></a><span id="Submitting_a_service_metadata_package"></span><span id="submitting_a_service_metadata_package"></span><span id="SUBMITTING_A_SERVICE_METADATA_PACKAGE"></span>サービス メタデータ パッケージの申請

モバイル ブロードバンド アプリのサービス メタデータの提出について詳しくは、「[サービス メタデータ パッケージの提出](https://msdn.microsoft.com/library/windows/hardware/dn247118.aspx)」をご覧ください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

- [デバイス メタデータ エクスペリエンスの作成](https://msdn.microsoft.com/library/windows/hardware/br230794.aspx)

- [デバイス メタデータ エクスペリエンスの管理](https://msdn.microsoft.com/library/windows/hardware/br230797.aspx)

- [バルク メタデータ パッケージの提出](https://msdn.microsoft.com/library/windows/hardware/hh801895.aspx)

- [デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法](https://msdn.microsoft.com/library/windows/hardware/br230786.aspx)

 

 






