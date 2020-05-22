---
title: モバイル ブロードバンド メタデータ作成ウィザードでのサービスの説明
description: モバイル ブロードバンド メタデータ作成ウィザードでのサービスの説明
ms.assetid: 0FA4945C-3CD9-4106-BC47-F89CEF168FDC
keywords:
- モバイル ブロードバンド メタデータ作成ウィザードでのサービスの説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eba754f1d11af03ab5d5605fd16304906b8dfb4
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769622"
---
# <a name="describe-your-service-in-the-mobile-broadband-metadata-authoring-wizard"></a>モバイル ブロードバンド メタデータ作成ウィザードでのサービスの説明

モデル名や製造元など、Windows でのサービスに関する説明情報を提供できます。

### <a name="to-provide-descriptive-information-about-a-service"></a>サービスに関する説明情報を提供するには

1. [**説明**] タブをクリックします。
2. 次のフィールドに入力します。
    - **サービス名**。 このオプションのフィールドは、Windows 8 では使用されません。
    - **サービスプロバイダー**。 Windows 接続マネージャーに表示されるオペレーター名です。
    - **サービス番号**。 サービスを一意に識別する GUID を指定します。 この GUID は、演算子の XML プロビジョニングを使用するときに演算子を識別するために使用されます。 デバイスメタデータパッケージを更新する場合、この GUID は同じままにしておく必要があります。
        **メモ** これは、デバイスメタデータパッケージのエクスペリエンス ID とファイル名とは異なります。 サービス番号の GUID の選択の詳細については、「[メタデータを使用したモバイルブロードバンドエクスペリエンスの構成の概要](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/using-metadata-to-configure-mobile-broadband-experiences)」を参照してください。

- **説明 1**. このオプションのフィールドは、Windows 8 では使用されません。
- **説明 2**. このオプションのフィールドは、Windows 8 では使用されません。

メタデータプロパティの詳細については、「[サービスメタデータパッケージのスキーマリファレンス](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata-package-schema-reference)」を参照してください。
