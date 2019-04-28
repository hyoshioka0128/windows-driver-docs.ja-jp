---
title: デスクトップ COSA/APN データベースの提出のテスト
description: デスクトップ COSA/APN データベースの提出のテスト
ms.assetid: 8f45dbf0-4f96-4d11-b2a2-41b9e75b5e9b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c3b835a15c6fd02855bf69f1e81344f6b6b7c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376992"
---
# <a name="testing-your-desktop-cosaapn-database-submission"></a>デスクトップ COSA/APN データベースの提出のテスト

Microsoft に APN 更新要求を送信する前に、MNO または MVNO APN エントリを送信しようとしていることを検証するため重要です。 Microsoft が、ネットワークへのアクセスは、送信される値は有効であり、動作させる必要がありますので正しくします。

## <a name="contact-your-microsoft-tam"></a>Microsoft TAM に問い合わせてください。

テストと、APN の更新を送信する最初の手順では、マイクロソフト カスタマー サービス & サポートで MS 解決ケースを TAM と協力します。 この場合は、追跡のためです。 MS 解決ケースを開くと、したら、サポート エンジニアに、次の情報を提供します。

-   APN 情報を含む完成したスプレッドシートです。

場合は、TAM ではありません。
-   (800) MICROSOFT (642-7676) を呼び出すことでは、マイクロソフト カスタマー サービス & サポートにお問い合わせください。
-   COSA/APN データベースを更新するサービスの担当者が必要な顧客に指示します。
-   スプレッドシートをサポート エンジニアに提供します。
-   要求された場合は、適切な製品として、Windows 8 または Windows 10 を指定します。

> [!NOTE]
> インシデント、クレジット カードを提供する必要がありますを課金されません。 

## <a name="test-your-submission-for-desktop-cosa"></a>デスクトップ COSA の提出をテストします。

Windows 10 バージョン 1703 以降では、このプロセスを使用します。

TAM に、APN 情報を含む、完成したスプレッドシートを送信すると後、Microsoft がプロビジョニング パッケージ (.ppkg) ファイルを作成してをインストールして、APN をテストできるようにした後に返送します。 

プロビジョニング パッケージ ファイルをインストールする方法の詳細については、次を参照してください。[プロビジョニング パッケージの適用](https://technet.microsoft.com/itpro/windows/deploy/provisioning-apply-package)します。

### <a name="modify-the-local-cosa-database-desktop-cosa"></a>ローカル COSA データベース (デスクトップ COSA) の変更します。

更新された COSA プロビジョニング パッケージ (PPKG)、APN 情報スプレッドシートを完了し、TAM に送信した後、Microsoft から受け取ったをテストする次の手順に従います。

次の手順では、Microsoft を適用し、テスト PPKG ファイルからのスクリプトが必要です。 次のリンクを使用して、スクリプトの最新バージョンをダウンロードする:<https://go.microsoft.com/fwlink/p/?linkid=866771>します。

#### <a name="apply-the-test-ppkg-file"></a>テスト PPKG ファイルを適用します。

> [!IMPORTANT]
> 次の操作を実行する前に、元のプロビジョニング パッケージのバックアップを作成します。 元のプロビジョニング パッケージが配置されているこちら:`%systemroot%\Provisioning\Cosa\Microsoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg`します。

1. 存在する場合は、デバイスから、SIM を削除します。
2. スクリプトと、新しい PPKG ファイルをローカル ディレクトリにコピーします。
3. 管理者特権のコマンド プロンプト ウィンドウを開き、スクリプトを含むディレクトリに変更します。
4. PPKG を適用するには、この構文でスクリプトを実行します。`ApplyCosaProvisioning.BAT -a <full path to the PPKG local directory>`します。
   1. たとえば次のようになります。`ApplyCosaProvisioning.BAT -a "C:\FromMicrosoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg"`
5. SIM を挿入し、プロビジョニングを待機します。

#### <a name="restore-the-original-ppkg-file"></a>元の PPKG ファイルを復元します。

> [!WARNING]
> Microsoft から受け取った新しい PPKG の検証が完了すると、次の手順で復元常にします。 元 PPKG に復元するには、Windows Update を使用して、最新の COSA 更新プログラムを受信するようされます。

1. 検証とは、SIM をデバイスから削除します。
2. 元の PPKG を復元するには、この構文でスクリプトを実行します。`ApplyCosaProvisioning.BAT -r`します。
3. 有効にする、読み取り元 PPKG プロビジョニング SIM に挿入します。

#### <a name="collect-logs-in-case-of-failure"></a>障害発生時のログを収集します。

テストのプロセス中にエラーが発生した場合のログを収集するには、次の手順を実行します。

1. デバイスから、SIM を削除します。
2. 開始するには、この構文でスクリプトを実行*netsh*ログ:`ApplyCosaProvisioning.BAT -l`します。
3. SIM を挿入し、プロビジョニングが失敗するまで待機します。
4. ログ記録を終了するツールの画面の指示に従います。
5. Zip 形式でログを Microsoft に送信します。

## <a name="test-your-submission-for-the-apn-database-apndatabasexml"></a>APN データベース (apndatabase.xml) の提出をテストします。

Windows 8、Windows 8.1、および Windows 10、Windows 10 バージョン 1703 より前に、のバージョンには、このプロセスを使用します。

Microsoft に提出する前に、APN エントリが動作することを確認できます 2 つの方法はあります。

-   [現在のプロファイルの APN 値の編集](#editprofile)

-   [ローカルの APN データベースを変更します。](#modifydatabase)

### <a href="" id="editprofile"></a> 現在のプロファイルの APN 値の編集

Apn の入力が、ネットワークに接続できることをテストする簡単な方法では、現在のプロファイルを編集し、プロファイルにテストを行う APN を挿入します。 このテストを実行するのには、次の手順を実行します。

> [!NOTE]
> このテストが記載されている完全な経験をシミュレートしません、[ローカル APN データベースの変更](#modifydatabase)セクション。 

1.  SIM をテストする APN 値で動作する PC に挿入します。

2.  PC、Windows、ログオンを有効にし、Windows 接続マネージャーを開きます。 モバイル ブロード バンド接続が表示されます。

3.  モバイル ブロード バンド接続を右クリックし、**接続プロパティを表示**します。

4.  このダイアログ ボックスにテストする APN の値を入力します。

5.  変更内容を保存して、モバイル ブロード バンド ネットワークに接続し直してください。

### <a href="" id="modifydatabase"></a>ローカルの APN データベースを変更します。

APN の更新を送信する前に、ローカルの APN データベースの編集またはテスト用の新しいハブを作成する必要があります。 これにより、密接にシミュレートする完全なエクスペリエンス Windows 接続マネージャーを使用する、APN 選択ロジックを完全にテストするため。

**ローカルの APN 接続のデータベースを変更します。**

1. **ローカルの APN データベース ファイルから既存の値をコピー** --、PC 上のローカルの APN データベースの既存のエントリを表示し、新しい XML ファイルにこれらのエントリをコピーします。 APN データベースのローカル コピー内の APN エントリを持ち、この手順をスキップし、空の XML ファイルを開始します。

2. **パブリッシュされた APN スキーマに従った XML ファイル内の値を変更**– APN エントリは、次のことを確認、 [APN データベースのスキーマ リファレンス](apn-database-schema-reference.md)します。

3. **ハードウェア Id を生成**-いずれかを指定するハードウェア Id または複数のハードウェア id 文字列をデータベース内の APN エントリに SIM 特性に一致します。 各文字列がで指定された、 [HardwareId](hardwareid-apnxml.md)要素。 Mbidgenerator.exe を使用して、ハードウェア Id を生成することをお勧めします。 詳細については、次を参照してください。 [mbidgenerator.exe を使用して、ハードウェア Id を生成する](using-mbidgeneratorexe-to-generate-hardware-ids.md)します。

4. **生成したファイルが公開されている APN データベース スキーマに準拠していることを検証**-スキーマの確認を生成したファイルが準拠していることを確認して、常に実行、 [APN データベースのスキーマ リファレンス](apn-database-schema-reference.md)します。

5. **新しいデータベースで、PC の APN 接続データベースを上書き**

   1.  管理者特権でコマンド プロンプトで、次のように入力します。 **cd %systemroot%\\system32**し、ENTER キーを押します。

   2.  型**takeown/f\\ 。ApnDatabase.xml**し、ENTER キーを押します。

   3.  型**icacls.\ApnDatabase.xml/grant %username%: F**し、ENTER キーを押します。

   4.  カスタマイズされたバージョンの ApnDatabase.xml ファイルをディレクトリにコピーします。

6. APN エントリがローカルの APN データベースに存在する検証します。

   1. 次のコマンドを実行して既存のモバイル ブロード バンド プロファイルがないことを確認します**netsh mb は、プロファイルを表示する。**

   2. モバイル ブロード バンド プロファイルが存在する場合は、入力**netsh mb プロファイル インターフェイス =&lt;インターフェイス名&gt;名 =&lt;プロファイル名&gt;**

   3. デバイスがプロビジョニングされているコンテキストを次のコマンドを実行してがないことを確認します: **netsh mb show provisionedcontext インターフェイス =&lt;インターフェイス名&gt;**

      **注**デバイス プロビジョニングのコンテキストを提供するかどうか、Windows はローカル APN データベースではなく、APN のプロビジョニングのコンテキストからを使用しは、APNs をテストすることはできません。 デバイス プロビジョニングのコンテキストにある場合は、プロビジョニングのコンテキストを提供しない別のデバイスを取得する必要があります。    

   4. Windows 接続マネージャーを開きます。 Wi-fi および範囲内にあるモバイル ブロード バンド ネットワークが表示されます。

   5. 携帯ネットワークを選択し、クリックして**Connect**します。

   6. SIM プロパティに一致する複数の APNs の場合は、正常に接続されるまで、Windows 接続マネージャーは、一致する APNs の各を試します。 接続なし、APNs の場合 Windows 接続マネージャーがエラーを表示またはカスタム APN エントリの画面を表示、ユーザーがカスタム APN を入力できるようにします。

      **注**APNs が試行される順序を決定する、APN データベースで指定した自動接続順を使用します。         

   7. APN データベースの 1 つだけの APN があれば、Windows はオペレーターのネットワークに自動的に接続します。

> [!NOTE]
> 適用されていた APN を確認できます Windows 接続マネージャーを開き、モバイル ブロード バンド ネットワークのエントリを右クリックし、をクリックして、接続プロファイル**プロパティ**します。 

