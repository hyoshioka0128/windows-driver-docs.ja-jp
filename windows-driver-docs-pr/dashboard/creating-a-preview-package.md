---
title: プレビュー パッケージの作成
description: プレビュー パッケージの作成
ms.assetid: 49880681-480d-4f2d-bf8f-d621ac275244
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09b7376a8df2c4f4aebdfd3f36bf04f430b00726
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67353915"
---
# <a name="creating-a-preview-package"></a>プレビュー パッケージの作成

作成したパッケージは、プレビュー用としてのみ提出することができます。 これによって、クライアント デバイスでのエクスペリエンスをテストし、適宜変更を加えたうえで、ライブ エクスペリエンスとしてリリースすることが可能となります。

## <a name="submitting-a-preview-package"></a>プレビュー パッケージの提出

プレビュー パッケージを提出する前にまず、会社に固有の PreviewKey を作成しておく必要があります。 プレビュー パッケージをダウンロードできるのは、PreviewKey を知っているユーザーだけです。

プレビュー パッケージのリリース プロセスは、他のパッケージをリリースするプロセスと基本的には変わりません。ただし、PreviewKey が必要であることがユーザーにわかるように、パッケージをプレビューとして指定する必要があります。

会社のパートナーによって提出されたプレビュー パッケージについては、その会社の PreviewKey が、以下の内容でレジストリ キーに設定されている必要があります。

- 記号の意味:HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Device Metadata

- 値の名前: DeviceMetadataPreviewKey

- 値の種類:REG\_SZ

- 値:&lt;自分の PreviewKey&gt;

### <a name="to-create-a-previewkey"></a>PreviewKey を作成するには

1. パートナー センターから、Microsoft アカウントを使用してダッシュボードにサインインします。

2. ウィンドウの左側の **[Device metadata]** (デバイス メタデータ) をクリックします。

3. **[Device metadata]** (デバイス メタデータ) ページの **[Manage preview key]** (プレビュー キーの管理) に、次のガイドラインに準拠した PreviewKey を入力します。

    - PreviewKey に使用できる文字数は、1 ～ 15 文字です。

    - 英数字を使う必要があります。 つまり、PreviewKey に使うことのできる文字は、アルファベットの大文字と小文字か数値に限られます。 PreviewKey に特殊文字を含めることはできません。

    - 既にあるどの PreviewKey とも異なっている必要があります。

    - 使用できる PreviewKey は会社ごとに 1 つだけです。

## <a name="related-topics"></a>関連トピック

[デバイス メタデータ エクスペリエンスを作成する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

[デバイス メタデータ パッケージを申請する (ダッシュボード ヘルプ)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)
