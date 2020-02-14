---
title: 製品データの取得
description: Microsoft ハードウェア API の以下のメソッドは、デベロッパー センター アカウントに登録されているハードウェア製品のデータを取得します。
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d881ea71051ac1c65c2c06207cef7ebab7953b1
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072163"
---
# <a name="get-product-data"></a>製品データの取得

*Microsoft ハードウェア API* の以下のメソッドを使用して、デベロッパー センター アカウントに登録されているハードウェア製品のデータを取得します。 API を使用するための前提条件など、Microsoft ハードウェア API の概要については、「[API を使用したハードウェア提出の管理](dashboard-api.md)」を参照してください。

```cpp
https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/
```

これらのメソッドを使用するには、製品をお客様自身のデベロッパー センター アカウントに用意しておく必要があります。 製品の申請を作成または管理する方法については、「[製品申請の管理](manage-product-submissions.md)」のメソッドを参照してください。

| 認証方法 | URI | 説明 |
|-|-|-|
|GET |`https://manage.devcenter.microsoft.com/v2.0/hardware/products/`|[すべての製品のデータの取得](get-all-products.md)|
|GET |`https://manage.devcenter.microsoft.com/v2.0/hardware/products/{productID}`|[特定の製品のデータの取得](get-a-product.md)|
|GET |`https://manage.devcenter.microsoft.com/v2.0/hardware/products/{productID}/submissions`|[製品のすべての申請に関するデータの取得](get-all-submissions.md)|
|GET |`https://manage.devcenter.microsoft.com/v2.0/hardware/products/{productID}/submissions/{submissionId}`|[製品の特定の申請に関するデータの取得](get-a-submission.md)|

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="data-resources"></a>データ リソース

製品データを取得するための Microsoft ハードウェア API のメソッドでは、次の JSON データ リソースが使われます。

### <a name="product-resource"></a>製品リソース

このリソースは、アカウントに登録されているハードウェア製品 (ドライバー) を表します。

```json
{
  "id”: 9007199267351834,
  “sharedProductId”: 1152921504606971100,
  “links”: [
    {
      “href": "https:// manage.devcenter.microsoft.com/api/v2.0/hardware/products/9007199267351834",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v2.0/hardware/products/9007199267351834/submissions",
      "rel": "get_submissions",
      "method": "GET"
    }
  ],
  "isCommitted": true,
  "isExtensionInf": false, "_comment": "THis field is deprecated and moved to submission resource",
  "deviceMetadataIds": [],
  "deviceType": "notSet",
  "isTestSign": false,
  "isFlightSign": false,
  "marketingNames": [
    "marketing name 1",
    " marketing name 2"
],
  "productName": "product name",
  "selectedProductTypes": {
    "windows_v100Server": "Unclassified",
    "windows_v100": "Unclassified"
},
  "requestedSignatures": [
    "WINDOWS_v100_X64_TH1_FULL",
    "WINDOWS_v63_X64"
  ],
  "additionalAttributes": {},
  "testHarness": "hlk",
  " announcementDate ": "2016-10-22T00:00:00Z",
}
```

このリソースには、次の値があります。

| 値 | 種類 | 説明 |
|:--|:--|:--|
| Id | Long | 製品のプライベート製品 ID |
| sharedProductId | Long | 製品の共有製品 ID |
| リンク | オブジェクトの配列 | 詳細については、「[リンク オブジェクト](#link-object)」を参照してください。 |
| isCommitted | ブール型 | 製品に少なくとも 1 つのコミットされた申請があるかどうかを示します  |
| isExtensionInf | ブール型 | (非推奨) 製品が拡張ドライバーかどうかを示します。 このフィールドは非推奨です。今後は使用しないでください。 isExtensionInf は申請レベルのプロパティに移動されました。 |
| deviceMetadataIds | GUID の配列 | デバイス メタデータの提出をドライバーにマップする GUID |
| deviceType | String | デバイスの種類を示します。 設定可能な値は、次のとおりです。<ul><li>“internal” - 内部コンポーネント、システムの一部として PC 内部に接続されるデバイス</li><li>“external” - 外部コンポーネント、PC に接続される外部デバイス (周辺機器)</li><li>“internalExternal” - その両方、内部的に (PC 内で) 接続できるほか、外部的にも (周辺機器として) 接続できるデバイス</li><li>“notSet” – データが存在しない</li></ul>|
| isTestSign | ブール型 | 製品がテスト署名されたドライバーかどうかを示します。 ドライバー パッケージのテスト署名の詳細については、「[WHQL Test Signature Program](https://docs.microsoft.com/windows-hardware/drivers/install/whql-test-signature-program)」(WHQL テスト署名プログラム) を参照してください。  |
| isFlightSign | ブール型 | 製品がフライト署名されたドライバーかどうかを示します。 フライト署名されたドライバーは、Windows Update を通じて公開できるテスト ドライバーです。 これらは、Windows Insider Program 用にサインアップしているコンピューターにのみ公開/インストールできます。 これらは、セキュア ブートを無効にすることなく、コンピューターにインストールできます。 これらは、Windows Insider Program の一部ではない、製品版のコンピューターにはインストールできません。|
| marketingNames | 文字列の配列 | 製品のマーケティング名またはエイリアス |
| productName | String | 作成中に指定されたドライバーの名前 |
| selectedProductTypes | ディクショナリ  | キーと値のペア (両方とも文字列)。 <ul><li>**Key** はオペレーティング システムのファミリー コードを表します。 オペレーティング システムのファミリのコードの一覧については、「[OS ファミリ コードの一覧](#list-of-operating-system-family-codes)」を参照してください。</li><li>**Value** は製品の種類を表します。 製品の種類の一覧については、「[製品の種類](#list-of-product-types)」を参照してください。</li></ul>|
| requestedSignatures | 文字列の配列 | 製品の認定対象となるオペレーティング システムの署名の一覧です。 すべてのオペレーティング システムの一覧については、「[OS コードの一覧](#list-of-operating-system-codes)」を参照してください。  |
| additionalAttributes | オブジェクト | 詳細については、「[その他の属性オブジェクト](#additional-attribute-object)」を参照してください。 |
| testHarness | string | 提出されたパッケージの種類。 設定可能な値は、次のとおりです。 <ul><li>hlk<li>hck</li><li>attestation</li><li>notset</li></ul>|
| announcementDate | datetime | Windows Server Catalog に製品が含められる日付 |

### <a name="submission-resource"></a>申請のリソース

このリソースは、製品の申請を表します。

```json
{
  "id": 1152921504621442000,
  "productId": 13635057453741328,
   "workflowStatus": {
      "currentStep": " finalizeIngestion",
      " state": " completed",
      " messages": []
    },
  "links": [
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v2.0/hardware/products/13635057453741329/submissions/1152921504621441944",
      "rel": "self",
      "method": "GET"
    }
  ],
  "commitStatus": "commitPending",
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "HARRY-Duatest2",
  "type": "derived"
}
```

このリソースには、次の値があります。

| 値 | 種類 | 説明 |
|:--|:--|:--|
| Id | long | 申請 ID |
| Productid | long | この申請が関連付けられているプライベート製品 ID |
| リンク | オブジェクトの配列 | 詳細については、「[リンク オブジェクト](#link-object)」を参照してください。 |
| 名前 | string | 申請名 |
| 種類 | string | 申請が最初の申請であるかまたは派生申請であるかを示します。 設定可能な値は、次のとおりです。 <ul><li>initial</li><li>derived</li></ul> |
| isExtensionInf | ブール型 | 申請が拡張ドライバーかどうかを示します |
| isUniversal | ブール型 | 申請がユニバーサル API テストに適合しているかどうかを示します。 ドライバーが宣言型かつユニバーサルである場合、そのドライバーは DCHU に準拠しています |
| isDeclarativeInf | ブール型 | 申請が宣言型 INVerif テストに適合しているかどうかを示します。 ドライバーが宣言型かつユニバーサルである場合、そのドライバーは DCHU に準拠しています |
| workflowstatus | オブジェクト | これは、特定の申請の詳細を取得する場合にのみ利用可能です。 このオブジェクトは、この申請のワークフローの状態を示しています。 詳細については、「[ワークフローの状態オブジェクト](#workflow-status-object)」を参照してください。  |
| ダウンロード | オブジェクト | これは、特定の申請のみの詳細を取得する場合にだけ利用可能です。 このオブジェクトは、申請に利用可能なダウンロードを示しています。 詳細については、「[リンク オブジェクト](#download-object)」を参照してください。 |

### <a name="workflow-status-object"></a>ワークフローの状態オブジェクト

このオブジェクトは、特定のエンティティのワークフローの状態を表します。

```json
{
      "currentStep": " finalizeIngestion",
      " state": " completed",
      " messages": []
    }
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
| currentStep | string | このエンティティの全体的なワークフローにおける現在のステップの名前。 <br>取り込み/パッケージの申請の場合、指定可能な値は次のとおりです (かっこ内に説明を示します)。<ul><li>packageInfoValidation (*パッケージのメタデータとコンテンツを検証*)</li><li>preparation (*処理のためにパッケージを準備*)</li><li>scanning (*マルウェアがないかどうかパッケージの内容をスキャン*)</li><li>validation (*テスト結果の検証*)</li><li>catalogCreation (*パッケージのセキュリティ カタログを作成*)</li><li>manualReview (*手動による評価が進行中*)</li><li>signing (*バイナリの署名*)</li><li>finalizeIngestion (*取り込みを完了して、署名されたファイルをダウンロードまたは公開できるように準備*)</li></ul>|
| State | string | 現在のステップの状態。 設定可能な値は、次のとおりです。<ul><li>notStarted</li><li>started</li><li>失敗</li><li>完了</li></ul> |
| Messages | array | (特に障害発生時に) 現在のステップに関するメッセージを提供する文字列の配列 |

### <a name="download-object"></a>オブジェクトのダウンロード

このオブジェクトは、特定の申請のダウンロードを表します。

```json
{
  "items": [
    {
      "type": "initialPackage",
      "url": "https://ingestionpackages.blob.core.windows.net/ingestion/dc55b8c6-a01c-40b6-b815-cac8bc08812a?sv=2016-05-31&sr=b&sig=ipjW3RsVC75lZrcEZRh9JmTX89L4gTIKkxwqv9F8Axs%3D&se=2018-03-12T15:32:10Z&sp=rl"
    },
    {
      "type": "derivedPackage",
      "url": "https://ingestionpackages.blob.core.windows.net/ingestion/6bd77dbf-a851-46d2-b703-29ea4efae006?sv=2016-05-31&sr=b&sig=O5XQf%2FzMbI2FFt5WwSUJWL1JbWY4JXXPRkCKAnX7IRs%3D&se=2018-03-12T15:32:10Z&sp=rl&rscd=attachment%3B filename%3DShell_1152921504621441930.hlkx"
    },
    {
      "type": "signedPackage",
      "url": "https://ingestionpackages.blob.core.windows.net/ingestion/0b83a294-c1d1-4136-82a1-dd52f51841e3?sv=2016-05-31&sr=b&sig=zTfxKJmaTwpbFol%2FpAKG0QuXJTTxm5aZ0F2wQQI8whc%3D&se=2018-03-12T15:32:10Z&sp=rl"
    },
    {
      "type": "certificationReport",
      "url": "https:// manage.devcenter.microsoft.com/dashboard/hardware/Driver/DownloadCertificationReport/29963920/13635057453741329/1152921504621441930"
    }
  ],
  "messages": []
}
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
| 項目 | array | ダウンロードの種類と、それぞれの URL の配列です。 詳細については、以下を参照してください。 |
| 種類 | string | ダウンロード可能なパッケージの種類。 設定可能な値は、次のとおりです。<ul><li>“initialPackage” – ユーザーがアップロードしたパッケージ (新しい申請の場合、パッケージのアップロードに使用する SAS URI をポイントします)</li><li>“derivedPackage” – 派生申請のためのシェル</li><li>“signedPackage” – Microsoft によって署名されているパッケージ</li><li>“certificationReport” – 署名された製品の認定レポート</li></ul>|
| Messages | array | ダウンロード可能なファイルについてのメッセージを提供する文字列の配列 |

### <a name="link-object"></a>リンク オブジェクト

このオブジェクトは、コンテナー エンティティの役立つリンクの一覧を表します

```json
{
      "href": "https:// manage.devcenter.microsoft.com/api/v2.0/hardware/products/9007199267351834",
      "rel": "self",
      "method": "GET"
    }
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
| Href | String | API を介してリソースにアクセスするための URL |
| Rel | String | リソースの種類。 設定可能な値は、次のとおりです。<ul><li>self – リンクは自身を指定</li><li>next_link – リンクは通常、改ページに使用される次のリソースを指定</li><li>get_submissions – リンクは製品のすべての申請を指定</li><li>commit_submission – リンクは申請のコミットを指定 </li><li>update_submission – リンクは申請の更新を指定 </li><li>update_shippinglabel – リンクは配送先住所ラベルの更新を指定  </li><li>driverMetadata - リンクはドライバー メタデータのダウンロードを許可するファイルを指定。 詳しくは、[ドライバー パッケージのメタデータ](driver-package-metadata.md)に関する記事をご覧ください。</li></ul>|
| 認証方法 | String | URL を呼び出すときに使用される http メソッドの種類。 設定可能な値は、次のとおりです。<ul><li>GET</li><li>POST</li><li>PATCH</li></ul>|

### <a name="additional-attribute-object"></a>その他の属性オブジェクト

このオブジェクトは、製品の種類がRAID コントローラー、記憶域コントローラーまたはサーバー仮想化検証プログラム (SVVP) の場合、製品に関する追加の属性を提供します。 このオブジェクトには、StorageController、RaidController、SVVP の 3 種類のオブジェクトのいずれかを含めることができます。

#### <a name="storagecontroller-object"></a>StorageController オブジェクト

| 値 | 種類 | 説明 |
|:--|:--|:--|
| biosVersion | string | ROM Bios のバージョン |
| firmwareVersion | string | ファームウェア バージョン |
| driverVersion | string | ドライバーのバージョン |
| driverName | string | ドライバ名 |
| deviceVersion | string | デバイス バージョン |
| chipsetName | string | チップセット名 |
| usedProprietary | boolean | 独自のドライバーでサポートされたマルチパス。 true の場合、proprietaryName および proprietaryVersion は必須です |
| proprietaryName | string | マルチパス ソフトウェア名 |
| proprietaryVersion | string | マルチパス ソフトウェア バージョン |
| usedMicrosoft | boolean | デバイス固有のモジュールによってサポートされた Microsoft MPIO。 true の場合、microsoftName および microsoftVersion は必須です |
| microsoftName | string | マルチパス ソフトウェア名 |
| microsoftVersion | string | マルチパス ソフトウェア バージョン |
| usedBootSupport | boolean | ブート サポート |
| usedBetterBoot | boolean | 2\.2TB より大きいブートのサポート。  true の場合、サポートされる UEFI バージョンおよびサポートされる ACPI バージョンは必須です |
| uefiVersion | string | サポートされる UEFI バージョン |
| acpiVersion | string | サポートされる ACPI バージョン |
| supportsSector4K512E | boolean | 4K/512e のセクター サイズをサポートします |
| supportsSector4K4K | boolean | 4K/4K のセクター サイズをサポートします |
| supportsDifferential | boolean | 差分 (高電圧差分) |

#### <a name="raidcontroller-object"></a>RaidController オブジェクト

| 値 | 種類 | 説明 |
|:--|:--|:--|
| firmwareVersion | string | ファームウェア バージョン |
| filterVersion | string | ドライバーのバージョン |
| driverVersion | string | フィルター バージョン |
| usedProprietary | boolean | 独自のドライバーでサポートされたマルチパス。 true の場合、proprietaryName および proprietaryVersion は必須です |
| proprietaryName | string | マルチパス ソフトウェア名 |
| proprietaryVersion | string | マルチパス ソフトウェア バージョン |
| usedMicrosoft | boolean | デバイス固有のモジュールによってサポートされた Microsoft MPIO。 true の場合、microsoftName および microsoftVersion が必須です |
| microsoftName | string | マルチパス ソフトウェア名 |
| microsoftVersion | string | マルチパス ソフトウェア バージョン |
| isThirdPartyNeeded | boolean | 接続に必要なサード パーティ製の Microsoft 以外のドライバー |
| isSES | boolean | SES (SCSI エンクロージャ サービス)。 SES が含まれているかどうかを示します。 SCSI (スモール コンピューター システム インターフェイス) とは、システムでデバイスを接続するサービス バスを表す標準の用語です。 SES は、SCSI エンクロージャ サービスの略です。 |
| isSAFTE | boolean | SAF TE (ANBll 仕様)。 SAF-TE が含まれているかどうかを示します。 ANBll は業界仕様です。 SAF-TE は、SCSI アクセス フォールト トレラント エンクロージャの略です。 SCSI (スモール コンピューター システム インターフェイス) とは、システムでデバイスを接続するサービス バスを表す標準の用語です。 |
| additionalInfo | string | 追加情報 |

#### <a name="svvp-object"></a>SVVP オブジェクト

| 値 | 種類 | 説明 |
|:--|:--|:--|
| productVersion | string | 製品バージョン |
| supportLink | string | サポート URL |
| guestOs | string | ゲスト OS。 設定可能な値は、次のとおりです。<ul><li>Windows Server 2008</li><li>Windows Server 2008 Release 2</li><li>Windows Server 2012</li><li>Windows Server 2012 R2 </li></ul>|
| processorArchitecture | string | ハードウェア プロセッサ アーキテクチャ。 設定可能な値は、次のとおりです。<ul><li>Xeon</li><li>Opteron</li><li>Itanium 2</li></ul>|
| maxProcessors | 整数 | VM 内の最大プロセッサ |
| maxMemory | 整数 | VM 内の最大メモリ (GB 単位) |

### <a name="list-of-product-types"></a>製品タイプの一覧

製品は次のタイプのいずれかになります。 この情報は、オペレーティング システムと一緒に使用して適用性を確認します。

* オールインワン
* タッチ対応のオールインワン
* オーディオ デバイス
* Bluetooth コントローラー
* Bluetooth コントローラー (非 USB)
* コンバーチブル タブレット
* デスクトップ
* デジタル メディア レンダラー
* デジタル メディア サーバー
* デジタル スチル カメラ
* デジタル ビデオ カメラ
* デ分散スキャン管理対応デバイス
* エンタープライズ WSD 多機能プリンター
* 指紋リーダー
* ゲーム コントローラ
* 汎用的なコントローラー
* ポータブル デバイス全般
* グラフィックス アダプター WDDM1.0
* グラフィックス アダプター WDDM1.1
* グラフィックス アダプター WDDM1.2
* グラフィックス アダプター WDDM1.2 DisplayOnly
* グラフィックス アダプター WDDM1.2 RenderOnly
* グラフィックス タブレット
* ハード ドライブ
* キーボード
* キーボードのビデオ マウス スイッチ
* LAN
* LAN (サーバー)
* LAN CS
* LAN 仮想マシン (サーバー)
* ノート PC
* タッチ対応ラップトップ
* LCD
* 光センサー
* 位置センサー
* メディア プレーヤー
* モバイル ブロードバンド CDMA
* モバイル ブロードバンド GSM
* 携帯電話
* 監視
* マザーボード
* モーション センサー Fusion
* 多機能プリンター
* 近距離近接通信
* ネットワーク メディア デバイス
* 光学式ドライブ
* ペン デジタイザー
* ポインティング描画
* プレゼンス センサー
* プリンター
* Projector
* リムーバブル記憶域
* ルーター
* スキャナー
* SDIO コントローラー
* Server (サーバー)
* サーバー仮想化検証プログラム
* 署名タブレット
* Smart Cards
* スマート カード リーダー
* 記憶域配列
* 記憶域コントローラー
* 記憶域スペース アダプター
* 記憶域スペース ダイレクト
* Tablet
* Touch
* タッチ モニター
* ウルトラモバイル PC
* タッチ対応ウルトラモバイル PC
* USB コントローラー
* USB ハブ
* WebCam
* WLAN
* WLAN CSB
* WSD 多機能プリンター
* WSD プリンター
* WSD スキャナー

### <a name="list-of-operating-system-family-codes"></a>オペレーティング システム ファミリ コードの一覧

次の表に、オペレーティング システム ファミリ コードとその説明を示します。

| OS ファミリ コード | 説明 |
|:--|:--|
| WindowsMe | Windows Me |
| Windows2000 | Windows 2000 |
| Windows98 | Windows 98 |
| WindowsNT40 | Windows NT 4.0 |
| WindowsXP | Windows XP |
| WindowsServer2003 | Windows Server 2003 |
| WindowsVista | Windows Vista |
| Windows2008Server | Windows Server 2008 |
| WindowsHomeServer | Windows Home Server |
| Windows7 | Windows 7 |
| Windows2008ServerR2 | Windows Server 2008 Release 2 |
| WindowsServerSolutions | Windows Server Solutions |
| Windows8 | Windows 8 |
| Windows8Server | Windows Server 2012 |
| Windows81 | Windows 8.1 |
| Windows81Server | Windows Server 2012 R2 |
| Windows_v100 | Windows 10 Threshold |
| Windows_v100Server | Windows Server Threshold |
| Windows_v100_RS1 | Windows 10 Anniversary Update |
| Windows_v100Server_RS1 | Windows Server 2016 |
| Windows_v100_RS2 | Windows 10 RS2 Update |
| Windows_v100Server_RS2 | Windows Server RS2 |
| Windows_v100_RS3 | Windows 10 RS3 Update |
| Windows_v100Server_RS3 | Windows Server RS3 |
| Windows_v100_RS4 | Windows 10 RS4 Update |
| Windows_v100Server_RS5 | Windows Server 2019 |
| Windows_v100_RS5 | Windows 10 RS5 x86 |
| Windows_v100_RS5 | Windows 10 RS5 x64 |
| Windows_v100_19H1 | Windows 10 19H1 更新プログラム |

### <a name="list-of-operating-system-codes"></a>オペレーティング システム コードの一覧

次の表に、オペレーティング システム コードとその説明を示します。

| OS コード | 説明 |
|:--|:--|
|WINDOWS_ME|Windows Me|
|WINDOWS_98|Windows 98|
|WINDOWS_2000|Windows 2000|
|WINDOWS_NT40|Windows NT 4.0|
|WINDOWS_XP|Windows XP|
|WINDOWS_XP_IA64|Windows XP IA64|
|WINDOWS_XP_X64|Windows XP X64|
|WINDOWS_XP_MEDIA_CENTER|Windows XP Media Center|
|WINDOWS_2003|Windows Server 2003|
|WINDOWS_2003_IA64|Windows Server 2003 IA64|
|WINDOWS_2003_X64|Windows Server 2003 X64|
|WINDOWS_VISTA|Windows Vista クライアント|
|WINDOWS_VISTA_X64|Windows Vista クライアント X64|
|WINDOWS_2008_SERVER|Windows Server 2008|
|WINDOWS_2008_SERVER_IA64|Windows Server 2008 IA64|
|WINDOWS_2008_SERVER_X64|Windows Server 2008 X64|
|WINDOWS_HOME_SERVER|Windows Home Server|
|WINDOWS_7|Windows 7 クライアント|
|WINDOWS_7_X64|Windows 7 クライアント x64|
|WINDOWS_2008_SERVER_R2_IA64|Windows Server 2008 Release 2 IA64|
|WINDOWS_2008_SERVER_R2_X64|Windows Server 2008 Release 2 x64|
|WINDOWS_SERVER_SOLUTIONS_X64|Windows Server Solutions x64|
|WINDOWS_8|Windows 8 Client|
|WINDOWS_8_X64|Windows 8 クライアント x64|
|WINDOWS_8_ARM|Windows 8 クライアント RT|
|WINDOWS_8_SERVER_X64|Windows Server 2012|
|WINDOWS_v63|Windows 8.1 クライアント|
|WINDOWS_v63_X64|Windows 8.1 クライアント x64|
|WINDOWS_v63_ARM|Windows 8.1 クライアント RT|
|WINDOWS_v63_SERVER_X64|Windows Server 2012 R2 x64|
|WINDOWS_v100_TH1_FULL|Windows 10 クライアント バージョン 1506 および 1511 (TH1)|
|WINDOWS_v100_X64_TH1_FULL|Windows 10 クライアント バージョン 1506 および 1511 x64 (TH1)|
|WINDOWS_v100_SERVER_X64_TH1_FULL|Windows Server 2016 x64 (TH1)|
|WINDOWS_v100_TH2_FULL|Windows 10 クライアント バージョン 1506 および 1511 (TH2)|
|WINDOWS_v100_X64_TH2_FULL|Windows 10 クライアント バージョン 1506 および 1511 x64 (TH2)|
|WINDOWS_v100_SERVER_X64_TH2_FULL|Windows Server 2016 x64 (TH2)|
|WINDOWS_v100_RS1_FULL|Windows 10 クライアント バージョン 1607|
|WINDOWS_v100_X64_RS1_FULL|Windows 10 クライアント バージョン 1607 x64|
|WINDOWS_v100_SERVER_X64_RS1_FULL|Windows Server 2016 x64 (RS1)|
|WINDOWS_v100_RS2_FULL|Windows 10 RS2 クライアント|
|WINDOWS_v100_X64_RS2_FULL|Windows 10 RS2 クライアント x64|
|WINDOWS_v100_RS3_FULL|Windows 10 RS3 クライアント|
|WINDOWS_v100_X64_RS3_FULL|Windows 10 RS3 クライアント x64|
|WINDOWS_v100_ARM64_RS3_FULL|Windows 10 RS3 クライアント ARM64|
|WINDOWS_v100_RS4_FULL|Windows 10 RS4 クライアント|
|WINDOWS_v100_X64_RS4_FULL|Windows 10 RS4 クライアント x64|
|WINDOWS_v100_ARM64_RS4_FULL|Windows 10 RS4 クライアント ARM64|
|WINDOWS_v100_SERVER_X64_RS5_FULL | Windows Server 2019 |
|WINDOWS_v100_RS5_FULL | Windows 10 RS5 x86 |
|WINDOWS_v100_X64_RS5_FULL | Windows 10 RS5 クライアント x64 |
|WINDOWS_v100_19H1_FULL |Windows 19H1 クライアント x86 |
|WINDOWS_v100_X64_19H1_FULL |Windows 19H1 クライアント x64 |
|WINDOWS_v100_ARM64_19H1_FULL | Windows 19H1 クライアント ARM64 |

## <a name="error-codes"></a>エラー コード

エラー コードは、API のすべての Web メソッドに適用されます。 要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| HTTP の状態 | 説明 |
|:--|:--|
| 400 - 要求が正しくありません | 要求が正しい形式ではありません (例: 正しくない要求の構文、無効な要求メッセージのフレーム、詐欺的な要求ルーティング) |
| 401 – 未承認 | 認証に失敗したか、指定されていません |
| 403 – 使用不可能 | リソースへのアクセスは許可されていません |
| 404 – ページ未検出 | 要求されたエンティティが見つかりません。 |
| 415 – サポートされていないメディアの種類です | ペイロードは、ターゲット リソースでこの方法によってサポートされていない形式です。 |
| 422 - 処理できないエンティティです | 検証エラー。 |
| 500 - インターネット サーバー エラー | API のサーバーで回復不能なエラーが発生しました。 |

機能の検証エラーがある場合、応答本文には次の機能のエラー コードのいずれかが含まれます。

| エラー コード | エラー メッセージ | 説明 |
|:--|:--|:--|
| InvalidInput |  | 入力の検証が失敗したときに返されます |
| RequestInvalidForCurrentState | 保留中の申請のみコミットできます | 保留中の状態でない申請にコミットが適用されたときに返されます |
| RequestInvalidForCurrentState | 最初の申請が既に存在します | 既に最初の申請があるドライバーに最初の申請が作成されたときに返されます |
| RequestInvalidForCurrentState | 最初の申請が作成されていないため、派生申請を作成することはできません | 最初の申請がないドライバーに派生申請が作成されたときに返されます |
| UpdateUnauthorized | 製品を更新する権限がありません | 共有された製品を更新できないため、共有 (再販売) された製品を更新しようとするときに返されます |
| UpdateUnauthorized | 最初の申請がなければ製品を更新できません | 最初の申請がない製品を更新しようとするときに返されます |
| UpdateUnauthorized | ワークフローが失敗したため、製品を更新できません | 失敗したワークフローがある製品を更新しようとするときに返されます |
| UpdateUnauthorized | インジェスト処理が完了した後で発表日を更新することはできません | インジェストが完了した後で発表日が更新されたときに返されます |
| UpdateUnauthorized | 現時点では製品名を更新することはできません。 もう一度やり直してください |  |
| UpdateUnauthorized | 申請を更新する権限がありません | 共有された製品を更新できないため、共有 (再販売) された製品の申請を更新しようとするときに返されます |
| UpdateUnauthorized | ワークフローが失敗したため、申請を更新できません | 失敗したワークフローがある申請を更新しようとするときに返されます |
| EntityNotFound | 申請が見つかりません | 存在しない申請をコミットしようとするときに返されます |
| EntityNotFound | 製品が見つかりません | 製品が存在しない申請を作成しようとするときに返されます |
| InvalidInput | 拡張機能ドライバーは、自動更新プログラムとして公開する必要があります。 IsAutoInstallDuringOSUpgrade または isAutoInstallOnApplicableSystems のいずれかを true にする必要があります。 | 拡張機能 INF の Windows Update 配送先住所ラベルが、isAutoInstallDuringOSUpgrade または isAutoInstallOnApplicableSystems を選択せずに作成された場合に返されます |
| InvalidInput | CHID は、HardwareIds が Windows 10 以降のオペレーティング システムである場合にのみ許可されます。 | Windows 10 以前の OS を対象とした配送先住所ラベルが、CHID を使用して作成された場合に返されます。 CHID による対象指定は、Windows 10 以降に対してのみ適用されます。 |
| InvalidInput | 別のワークフローが進行中のときには配送先住所ラベルを更新できません。 もう一度お試しください。 | 前のワークフローがまだ進行中のときに配送先住所ラベルを更新しようとすると返されます。 |
| RequestInvalidForCurrentState | 公開用の配送先住所ラベルをインボックス ドライバーやシステムの種類に対して作成することはできません。 できるのは、配送先住所ラベルを共有することだけです。 | Windows Update の配送先住所ラベルを、インボックス ドライバーまたはシステム上で作成しようとした場合に返されます。 |
| RequestInvalidForCurrentState | 申請の配送先住所ラベルを作成する準備がまだできていません。 しばらくしてからやり直してください。 | 準備や事前処理が完了していない段階で配送先住所ラベルを作成しようとしたときに返されます。 |

## <a name="see-also"></a>関連項目

* [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
