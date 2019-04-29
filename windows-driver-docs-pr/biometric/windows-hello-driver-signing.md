---
title: Windows こんにちはフィンガー プリント ドライバー署名の処理
description: Windows こんにちはフィンガー プリント ドライバー署名の処理
ms.assetid: 803f4326-32ce-44b4-a2fb-6c6f245c3728
keywords:
- 生体認証ドライバー WDK、windows こんにちは
- 生体認証ドライバーへの署名
ms.author: dawnwood
ms.date: 07/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c2ad4afc2031afb34057ad75f053c9065ff830c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328353"
---
# <a name="windows-hello-steps-to-submit-a-fingerprint-driver"></a>Windows Hello:フィンガープリント ドライバーを送信する手順


## <a name="submitting-a-fingerprint-driver-for-windows-hello-compatibility"></a>Windows こんにちはの互換性のためのフィンガー プリント ドライバーを送信します。 
Microsoft には、Windows こんにちは品質ガイドラインに準拠する生態認証センサーに関して新しい要件が導入されています。 新しい手動レビュー プロセスは、Windows こんにちはと相互運用する承認を取得する必要があります。 プロセスが OS に適用されます、特定の Windows デベロッパー センター経由で取得したシグネチャのチェック (ここで: https://developer.microsoft.com/) をこのドキュメントでは、プロセスの中でのみ取得できます。 作成され、6/1/17 の前に、WHQL によって署名されているドライバーが grandfathered します。 この日以降後はこの署名を取得できません新規および更新されたドライバーは、Windows こんにちはとまたは実施日後に、Window 10 バージョン 1703 では機能しません。

ドライバーには常に Windows こんにちはの署名の取得を手動で承認が行われます。 承認済みのドライバー更新プログラムは、高速化の承認の前の送信を参照できます。 ドライバーは新しいセンサーに適用される場合、またはその影響まで、FRR、またはプレゼンテーション攻撃の検出、対応するエンジンへの変更が発生した場合、新しいレビューを受ける必要があります。 

生体認証の署名の実施日は、6/1/2017、その後、自己署名が含まれていないドライバーは読み込まれません、Windows こんにちはでは動作しなくです。

### <a name="step-one-create-a-biometric-driver"></a>手順 1:生体認証ドライバーを作成します。
生体認証ドライバーを作成する次の手順に従います。 https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-service-api-portal

### <a name="step-two-test-your-sensor-and-self-validate"></a>手順 2:センサーをテストし、自己を検証
Self は、センサーと Microsoft の生体認証の要件を満たしているされ、テンプレートの指紋セキュリティ レビューの結果を報告することを確認するドライバーを検証します。 要件とテンプレートのドキュメントは、Connect で指紋パートナー パッケージ内で確認できます。 接続にアクセスしない場合は、Microsoft の担当者に問い合わせてください。

### <a name="step-three-modify-the-driver-configuration-xml-file"></a>手順 3:ドライバーの構成 xml ファイルを変更します。
バージョン 1703 指紋 HLK テストがいることを確認するチェックは、ドライバーは、Windows 10 を送信するときに、<vendorCompliance>と<securityReview>タグは、次のフィールドに含まれています。

**bugId**:送信は、まったく新しいセキュリティ レビュー中である場合は、以前に承認されたセキュリティ情報の確認または 0 を格納する前の HLK 送信の ID 番号。

**updateExistingSubmission**: 更新プログラムは、セキュリティに関する確認と false の場合に行われている前の送信、送信が機能している場合に true それ以外の場合。

#### <a name="example"></a>例
 ```cpp
<?xml version="1.0" encoding="utf-8"?>
<bioTestConfiguration version="0" runOptional="false" runInteractive="true" abortOnFailure="false" manualStep="false" priority="3" logType="WTT">
  <vendorCompliance>
    <securityReview bugId="12345678" updateExistingSubmission="true"/>
  </vendorCompliance>
  <testSuites>
    <testSuite deviceRequired="false" id="StorageAdapter">
      <library>storagetest.dll</library>
      <description>storage Adapter Test Suite</description>
    </testSuite>
  </testSuites>
  <deviceInfo>
         <sensorAdapterLib>WinbioSensorAdapter.dll</sensorAdapterLib>
         <engineAdapterLib>vcsWBFEngineAdapter.dll</engineAdapterLib>
         <storageAdapterLib>winbiostorageadapter.dll</storageAdapterLib>
         <indicatorSupported>0</indicatorSupported>
         <supportedModes>
             <supportedMode>0x01</supportedMode>
         </supportedModes>
         <supportedPurposes>
             <supportedPurpose>0x01</supportedPurpose>
             <supportedPurpose>0x02</supportedPurpose>
             <supportedPurpose>0x04</supportedPurpose>
         </supportedPurposes>
  </deviceInfo>
</bioTestConfiguration>
 ```
### <a name="step-four-modify-the-driver-configuration-inf"></a>手順 4:ドライバーの構成を変更する inf
生体認証ドライバー パッケージは、必要な Windows こんにちは署名を取得し、WU にアップロードする新しいデベロッパー センター ポータルに送信する必要があります。 パッケージは、アダプターの dll のデジタル署名の取得を適切に指定するドライバーの INF ファイルに特定のプロパティを含める必要があります。 次の例では、アダプター バイナリとその関連するライブラリの略歴署名を取得する書式設定を示します。

たとえば、ドライバー パッケージには、センサー、エンジン、および記憶域アダプターを sensor.dll、engine.dll、およびとする storage.dll をそれぞれ、という名前が含まれているし、stringparser.dll 読み込まれる 1 つ、しごとに、自己署名を取得する INF ファイルする必要がありますが含まれて、次のコンポーネント:

```cpp
[SignatureAttributes]
sensor.dll = SignatureAttributes.WindowsHello
engine.dll = SignatureAttributes.WindowsHello
storage.dll = SignatureAttributes.WindowsHello
stringparser.dll = SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello = true
```

この手順は、ドライバーが適切な証明書を受け取ることを確認する最も重要なのです。 サード パーティ製生体認証のアダプターのすべてのファイルとこれらのアダプターによって読み込まれる任意のサード パーティ製 dll は、ラベル付けおよびデベロッパー センターに送信されたときに、生体認証署名を取得する場合は、この方法で含まれている必要があります。

### <a name="step-five-run-the-hlk-test-suite"></a>手順 5:HLK テスト スイートを実行します。
HLK テストが上記の変更手順 3 と 4 で行われたと確認の構成情報がない場合は失敗します。
HLK studio での最終的な HLK をパッケージ化するときに、補足ファイルとしてバグの送信のセキュリティ レビュー テンプレートが含まれます。

### <a name="step-six-submit-the-driver-package-and-hlk-logs"></a>手順 6:ドライバー パッケージと HLK ログを送信します。
レビュー用のデベロッパー センターにパッケージ化された HLK ファイルを送信します。 手動での確認プロセスになったときに、Microsoft 内で、機能チームは、送信の通知されます。 チームは自己検証済みの情報が Microsoft の生体認証の要件を満たしているかどうかを確認する HLK パッケージで送信されたテンプレートを確認します。

### <a name="step-seven-wait-for-microsoft-approval-and-signing"></a>手順 7:Microsoft 承認および署名のための待機
すべての生体認証要件を満たしている限り、Microsoft の送信を承認する生体認証の署名の取得は、ドライバーが Windows こんにちはで動作する証明書ではありません。 たとえば、ファイルを除外して、署名のチェックは inf 構成ファイルで可能性があります。 時にこのファイルが読み込まれている場合は、OS は、署名を強制し、読み込みに失敗、ドライバーは、Windows こんにちはでは動作しません。 集合的なシステムで動作することを確認するには、IHV と OEM によって署名されたドライバーをテストする必要があります。

### <a name="step-eight-update-an-existing-driver"></a>手順 8:既存のドライバーを更新します。
以前に署名されたドライバーの更新プログラムにする必要がある場合は、手順 3 で更新されたドライバーのドライバーの構成 xml には、updateExistingSubmission フィールドへの入力を指示します。
更新プログラムが grandfathered ドライバーに行われたされている場合、同じ手順を使用してください。 フィールドは、grandfathered ドライバーの送信 ID に設定する必要があり、updateExistingSubmission フィールドを設定する必要がありますを true にします。
ドライバーの構成 xml は、送信されたドライバー パッケージに含める必要があります。

## <a name="related-topics"></a>関連トピック


[Windows Hello 顔認証](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-hello-face-authentication)

[Windows Hello](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-hello)

[生体認証デバイスの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/biometric/)


