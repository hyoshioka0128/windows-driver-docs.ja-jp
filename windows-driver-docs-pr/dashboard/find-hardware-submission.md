---
title: ハードウェア申請の検索と管理
author: dimanjar
description: テキストを使って検索するか、キーワード検索でドライバー属性を選択することで、特定の Windows ハードウェア申請を検索する方法について説明します。
ms.author: dimanjar
ms.topic: article
ms.date: 09/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48dd2f115aa4d5c8cfad6e9e9e56842fd64e7a80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518999"
---
# <a name="find-a-hardware-submission"></a>ハードウェア申請を検索する

お客様の組織によって送信されたすべてのハードウェア申請は、ハードウェア ダッシュボードの **[ドライバー]** ページに表示されます。 特定のハードウェア申請を検索するには、次のいずれかの方法を使うことができます。

- プレーン テキスト検索

- ドライバー属性によるキーワード検索

## <a name="plain-text-search"></a>プレーン テキスト検索

テキスト ボックスには、任意の検索語句を入力できます。 ダッシュボードでは、次のいずれかのフィールド内の語句に一致する単語を含んだエントリが返されます。

- 製品 ID (プライベートと共有)

- 申請 ID

- 製品名

- 申請名

- ハードウェア ID

- INF 名

- オペレーティング システム コード

たとえば、検索語句 **mydriver** を指定した場合は、次の製品名を使った申請が返されます: *mydriver 1*、*new mydriver* および *old mydriver 2*、 *mydriver1* および *mydriver_new*。

## <a name="keyword-search"></a>キーワード検索

キーワード検索を使用して、ドライバー属性によってドライバーを検索できます。 検索ボックスにアットマーク (**\@**) を入力した場合、ダッシュボードには使用可能な属性の一覧が表示されます。 

![ハードウェア ダッシュボードの [ドライバー] ページのスクリーンショット (テキスト ボックスに @ 記号が入力されています)。 @ 記号に下に、使用可能な属性の一覧が表示されています。](images/ampersand-search.png)

@ 記号の後にテキストを入力すると、その条件に応じて一覧の内容が絞り込まれます。 事前設定された値のいずれかをクリックすると、その項目が **(@*ParameterName*: "")** という形式で検索ボックスに表示されます。 引用符 (**""**) の間に文字列を入力する以外に、パラメーター名や形式を変更することはしないでください。 検索語句は、完全な検索値でも、部分的な検索値でもかまいません。 たとえば、オペレーティング システム コードでドライバーを検索する場合は、次のいずれかを使用できます。

**@OperatingSystemCode:"Windows 10 RS4 Client x64"** 

または

**@OperatingSystemCode:"Windows 10 RS4"**

複数の属性を使用して検索することもできます。 複数の属性による検索は、AND 演算子を使った場合のにように動作します。 たとえば、製品名と申請の状態の両方 (**@ProductName:"test" @SubmissionStatus:"Failed"**) を検索した場合、ダッシュボードには製品名と申請の状態の**両方**に一致するレコードだけが返されます。

![ハードウェア ダッシュボードの [ドライバー] ページのスクリーンショット (@ProductName:"test" および @SubmissionStatus:"Failed" という 2 つの属性が入力されています)。 いずれの検索結果も、製品名に "test" が含まれ、申請の状態に "Failed" が含まれています。](images/two-attribute-search.png)

キーワード検索には、次のドライバー属性を使用できます。

|パラメーター|種類|設定可能な値|
|----|----|----|
|ProductID |数値|17 桁のプライベート製品 ID|
|SharedProductID |数値|19 桁の共有製品 ID|
|ProductName |Text|
|CertificationType |Text|Attestation (構成証明)、HCK、HLK、WLK|
|Permission (アクセス許可) |Text|Author (作成者)、Publisher (発行元)|
|SubmissionID |数値|19 桁の申請 ID|
|SubmissionName |Text|
|SubmissionType |Text|Initial (初期)、Derived (派生)|
|SubmissionStatus |Text|Complete (完了)、Failed (失敗)、NotSet (未設定)、Processing (処理中)、Ready (準備完了)|
|IsExtensionDriver |ブール値|False、True|
|IsUniversalDriver |ブール値|False、True|
|IsDeclarativeDriver |ブール値|False、True|
|INFName |Text|
|HardwareID |Text|
|OperatingSystemCode |Text|[OS コードの一覧](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-product-data#list-of-operating-system-codes)|

## <a name="search-results"></a>検索結果

ダッシュボードに表示される検索結果には、検索語句に一致するドライバー申請の一覧が示されます。

> [!NOTE]
> ハードウェア ダッシュボードでは、パッケージの受け入れが完了した後にエンティティが作成されます。 そのため、パッケージの受け入れが完了するまでは、ドライバー申請は検索結果に表示されません。

検索結果で**プライベート製品 ID** をクリックすると、ドライバーの概要ページに移動します。 そのページで、ドライバーの申請に関する情報を確認できます ([DUA プロセス](https://docs.microsoft.com/windows-hardware/test/hlk/user/create-a-driver-only-update-package)を通じた申請の更新、配送先住所ラベルの表示、作成、編集、署名済みファイルのダウンロード)。

### <a name="important-points"></a>重要なポイント

1. 特定のパラメーターを同じキーワード検索で複数使用することはできません。 たとえば、(**@ProductName:"test" @ProductName:"system"**) を検索するとエラーが発生します。

2. 現在のところ、**Submission Created Date (申請の作成日)** パラメーターや **Source (ソース)** パラメーターを使用して検索することはできません。 これらは現時点では使用できません。

3. 既定では、検索結果は**申請の作成日**を基準に降順で並べ替えられます。 列タイトルのフィールドをクリックすると、並べ替えを変更することができます。

4. 製品名やハードウェア ID を検索する場合は、完全な検索文字列を使用してください。 これらのフィールドにワイルドカード演算子を使用する必要がある場合、特殊文字 (英数字以外の文字) を使用することは避けてください。
