---
title: 手順 4 UWP デバイス アプリのデバイス メタデータをテストします。
description: ここでは、テストする方法デバイス メタデータ UWP デバイス アプリをローカルで、Windows デベロッパー センター ダッシュ ボードに送信する前に説明します。
ms.assetid: C1DA36DE-DB89-4A2A-8B9F-DF2A279D3EDD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac63ded86f4c48343fd3073d3eb55d3bdc35984a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348365"
---
# <a name="step-4-test-the-device-metadata-for-your-uwp-device-app"></a>手順 4:UWP デバイス アプリのデバイス メタデータをテストします。


![デバイス アプリのワークフロー、手順 4](images/4-device-app-workflow.png)

ここでは、テストする方法デバイス メタデータ UWP デバイス アプリをローカルで、Windows デベロッパー センター ダッシュ ボードに送信する前に説明します。

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**  このトピックはステップ バイ ステップの一連の一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>始める前に


これで、デバイスが適切に動作するかをテストできるように、ローカル コンピューター上のローカル デバイスのメタデータ ストアにデバイスのメタデータをデプロイできます。 デバイスのメタデータが配置されると、Windows デベロッパー センター ダッシュ ボードに、送信された場合と同じ方法を動作する必要があります。 たとえば、デバイスのメタデータ内のデバイスで自動再生が有効な場合、デバイスが接続されているときの自動再生ハンドラーでは動作します。 モデルまたはパブリッシャーの名前を変更する場合も表示これらの変更を確認することができます。

デバイスのメタデータをテストする前に、デバイス メタデータをデプロイするコンピューターに Microsoft Store アプリをインストールしてください。

## <a name="span-iddeployyourdevicemetadatalocallyspanspan-iddeployyourdevicemetadatalocallyspanspan-iddeployyourdevicemetadatalocallyspandeploy-your-device-metadata-locally"></a><span id="Deploy_your_device_metadata_locally"></span><span id="deploy_your_device_metadata_locally"></span><span id="DEPLOY_YOUR_DEVICE_METADATA_LOCALLY"></span>デバイスのメタデータをローカルでの配置します。


デバイスのメタデータをテストする前に、ローカル デバイスのメタデータ ストアに配置する必要があります。 選択してこれを行う、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスを使用してまたはデバイスのメタデータを作成するとき、**デバイス メタデータの作成ウィザード**デバイス メタデータを作成した後。

**デバイス メタデータの作成ウィザードを使用してデバイス メタデータを展開するには**

1.  開く、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86。
2.  **ツール** メニューのをクリックして**メタデータ パッケージの展開**します。
3.  .Devicemetadata ms ファイルを参照し、**開きます。**
4.  ユーザー アカウント制御 ダイアログ ボックスが表示されたら、クリックして**はい**します。
5.  デバイスのメタデータが展開された後を示すメッセージが表示されます**デバイス メタデータ パッケージは、このコンピューターのローカル メタデータ ストアに正常にコピーされました**します。 デバイスのメタデータをテストする準備ができました。

## <a name="span-idvalidateyourdevicemetadataspanspan-idvalidateyourdevicemetadataspanspan-idvalidateyourdevicemetadataspanvalidate-your-device-metadata"></a><span id="Validate_your_device_metadata"></span><span id="validate_your_device_metadata"></span><span id="VALIDATE_YOUR_DEVICE_METADATA"></span>デバイスのメタデータを検証します。


使用して UWP デバイスのアプリまたはデバイスに対して、デバイスのメタデータを検証することができます、**デバイス メタデータの作成ウィザード**します。

**デバイス メタデータの作成ウィザードを使用して、デバイスのメタデータを検証するには**

1.  開く、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86。
2.  クリックして**検証メタデータ**します。
3.  **選択メタデータ パッケージを検証する**ページで、次の操作を行います。
    -   下、**デバイス メタデータ パッケージ**見出しで、をクリックして**参照**、.devicemanifest ms ファイルを選択するかクリックして**ローカル メタデータ ストアから選択**したかどうかは既にデバイスのメタデータをローカルにデプロイされます。
    -   UWP アプリに対して検証する場合は、選択、 **UWP デバイスのアプリに対するデバイス メタデータ パッケージの検証**チェック ボックスをオンにし**参照**Microsoft Store アプリ パッケージ (.appx) を選択します。
    -   デバイスに対して検証する場合は、選択、**デバイスに対するデバイス メタデータ パッケージの検証** チェック ボックスをクリックします**デバイスからを選択します**お使いのデバイスを選択し、クリックして**ok をクリックします。**

4.  **[検証]** をクリックします。
5.  検証が完了すると、レポートを保存することができます。 **[閉じる]** をクリックします。
    **注意**  「エクスペリエンスの ID が一致しないアプリ パッケージで storeManifest.xml とデバイスのメタデータ ファイルで packageInfo.xml」と答えると検証レポートでエラーが発生する可能性があります。 このメッセージは無視しても問題ありません。

     

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>次の手順


[手順 5:アプリを送信します。](step-5--submit-the-app.md)

 

 





