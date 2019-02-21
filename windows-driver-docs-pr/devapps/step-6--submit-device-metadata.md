---
title: UWP デバイス アプリの手順 6 送信デバイス メタデータ
description: このトピックでは、Windows デベロッパー センター ハードウェア ダッシュ ボードに UWP デバイス アプリのデバイス メタデータを送信する方法について説明します。
ms.assetid: 5A4A371E-42A2-43C8-A496-CC3C38C17182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16e75953f87c5fb48ee01edb45ff87bbd867eca9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531005"
---
# <a name="step-6-submit-device-metadata-for-your-uwp-device-app"></a>手順 6:UWP デバイス アプリのデバイス メタデータを送信します。


![デバイス アプリのワークフロー、手順 6](images/6-device-app-workflow.png)

このトピックでは、Windows デベロッパー センター ハードウェア ダッシュ ボードに UWP デバイス アプリのデバイス メタデータを送信する方法について説明します。

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**  このトピックはステップ バイ ステップの一連の一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>開始する前に


ハードウェア ダッシュ ボードに、デバイス メタデータ パッケージを送信する 2 つの方法はあります。

-   ハードウェア ダッシュ ボードを個別に .devicemanifest ms ファイルを送信できます。
-   .Devicemanifest ms の複数のファイルをまとめてパッケージ化し、一括送信パッケージとしてのハードウェア ダッシュ ボードに送信できます。 使用して一括送信パッケージを作成することができます、**デバイス メタデータの作成ウィザード**します。

両方の方法では、ハードウェア ダッシュ ボードに送信する前に、ファイルが署名されている必要があります。 使用してこれを行う、**デジタル署名ウィザード**します。 開くには、**デジタル署名ウィザード**から、**デバイス メタデータの作成ウィザード**、 をクリックして**ツール**、 をクリックし、**署名ウィザード**.

## <a name="span-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespancreating-a-bulk-submission-package"></a><span id="Creating_a_bulk_submission_package"></span><span id="creating_a_bulk_submission_package"></span><span id="CREATING_A_BULK_SUBMISSION_PACKAGE"></span>一括送信パッケージを作成します。


使用することができます、**一括パッケージ ウィザード**ハードウェア ダッシュ ボードには、複数の devicemanifest ms ファイルを一度に送信できる一括送信パッケージを作成します。 使用する、**デバイス メタデータの作成ウィザード**を開く、**一括パッケージ ウィザード**します。

**一括送信パッケージを作成するには**

1.  **デバイス メタデータの作成ウィザード**、 をクリックして**ツール**、 をクリックし、**一括パッケージを作成する**します。
2.  **一括パッケージ ウィザード**、.devicemanifest ms ファイルごとに、次の操作を行います。
    -   クリックして**メタデータ パッケージを追加**します。
    -   .Devicemanifest ms ファイルを参照し、 **OK**します。

3.  選択、**プレビュー**プレビュー モードで送信する各 .devicemanifest ms ファイルの横にあるチェック ボックス。
4.  すべての .devicemanifest ms ファイルを追加した後にをクリックして**次**します。
5.  **デバイス エクスペリエンスの情報を指定** ページで、以下を追加します。
    -   **名前が発生する**お客様の会社によって送信された他の操作名の間で一意の名前にする必要があります。
    -   **認定**ハードウェアの提出がこの送信に関連付けられているかを示します。 関連付けられているハードウェアの提出がある場合は、選択**このデバイスには、関連するハードウェアまたは unclassified 送信**します。
    -   **ロゴの送信 Id**ハードウェア ダッシュ ボードの提出 Id を含める必要があります。
    -   **エクスペリエンスの更新**する前に、エクスペリエンスが送信された場合に選択する必要があります。

    **注**  UWP デバイス アプリのデバイス メタデータを送信する前に、デバイスを認定する必要があります。

     

6.  **提出用の準備一括パッケージ**] ページで [**署名ウィザードの起動**を開始する、**デジタル署名ウィザード**、一括のデジタル署名に使用します。提出パッケージ。

ハードウェア ダッシュ ボードへのデバイス メタデータ パッケージの送信についての詳細については、次を参照してください。[デバイス メタデータ](https://msdn.microsoft.com/library/windows/hardware/br230800.aspx)します。

 

 





