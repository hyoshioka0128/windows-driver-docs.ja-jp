---
title: 手順 3 を Microsoft Store のデバイスのアプリ エクスペリエンスの ID を追加します。
description: このトピックでは、UWP デバイスのアプリ エクスペリエンスの ID を追加する方法について説明します。
ms.assetid: D114C916-EADE-4C08-BF7E-628D2FA5AACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4817a2c5c8f6395d5c0e30b47f877ab95954a435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356636"
---
# <a name="step-3-add-an-experience-id-to-the-microsoft-store-device-app"></a>手順 3:Microsoft Store のデバイスのアプリに、エクスペリエンスの ID を追加します。


![デバイス アプリのワークフロー、手順 3](images/3-device-app-workflow.png)

このトピックでは、UWP デバイスのアプリ エクスペリエンスの ID を追加する方法について説明します。 *ID エクスペリエンス*GUID は、デバイス メタデータ パッケージを一意に識別する; は必須では自動インストールの場合、アプリが構成されているかどうかは、[プリンター用の UWP デバイス アプリ](uwp-device-apps-for-printers.md)と[カメラ](uwp-device-apps-for-webcams.md)します。

**ヒント:**  特権を持つアプリとしてアプリを指定し、自動インストールが構成されていない場合は、この手順をスキップすることができます。

 

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**  このトピックはステップ バイ ステップの一連の一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>始める前に


この手順で作成された StoreManifest.xml ファイルが必要です、[前の手順](step-2--create-device-metadata.md)します。 StoreManifest.xml ファイル エクスペリエンスの ID を指定します

## <a name="span-idaddstoremanifestxmltoyourprojectspanspan-idaddstoremanifestxmltoyourprojectspanadd-storemanifestxml-to-your-project"></a><span id="add_storemanifest.xml_to_your_project"></span><span id="ADD_STOREMANIFEST.XML_TO_YOUR_PROJECT"></span>StoreManifest.xml をプロジェクトに追加します。


操作 ID は StoreManifest.xml ファイルで指定されます。 この ID は、デバイスのメタデータに、アプリをリンクします。

**重要な**  とソリューションのルート フォルダーではなく、アプリのプロジェクトのルート フォルダーに、StoreManifest.xml ファイルを格納する必要があります。

 

**StoreManifest.xml をプロジェクトに追加するには**

1.  **ソリューション エクスプ ローラー**プロジェクトを右クリックし、選択、**追加&gt;既存項目の**します。
2.  **既存項目の追加** ダイアログ ボックスで、選択、StoreManifest.xml ファイルで作成した、[前の手順](step-2--create-device-metadata.md)します。
3.  プロジェクトに追加された後、StoreManifest.xml ファイルのプロパティを確認します。 右クリックし、 **StoreManifest.xml**ファイルおよび選択**プロパティ**します。 これを強調表示、**プロパティ**ウィンドウ。
4.  **プロパティ**ウィンドウで、いることを確認、**ビルド アクション**プロパティと等しい**コンテンツ**と**出力ディレクトリにコピー**プロパティ等しい**コピーしない**します。

StoreManifest.xml ファイルに関する詳細については、次を参照してください。 [StoreManifest スキーマ リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=307124)します。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>次の手順


[手順 4:テスト デバイス メタデータ](step-4--test-device-metadata.md)

 

 





