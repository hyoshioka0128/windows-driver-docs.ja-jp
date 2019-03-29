---
title: 新しいハードウェア申請の作成
description: 新しいハードウェア申請の作成
ms.assetid: 3F433F0A-422C-46E5-B59E-8DB4AC537F01
ms.date: 04/20/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 577e467d1248a0b8e734136e63c65b6645792e2c
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463820"
---
# <a name="create-a-new-hardware-submission"></a>新しいハードウェア申請の作成

Windows 10 用の Windows ハードウェア互換性プログラム (または以前のオペレーティング システム用の個別の認定プログラム) に対してハードウェアを準備するには、**.hlkx** ファイル (Windows 10 用) または **.hckx** ファイル (以前のオペレーティング システム用) を作成して提出する必要があります。 このファイルは、Windows HLK Studio (または以前のオペレーティング システムの場合は、Windows HCK Studio) を使って作成され、該当する製品に関するすべてのテスト結果、ドライバー、シンボルが格納されます。 このファイルを提出することによって、ダッシュボードからテスト結果を確認し、テストされたドライバーを評価し、Microsoft のデジタル署名済みのカタログ ファイルを返すことができます。

## <a name="to-create-a-submission-file"></a>提出ファイルを作成するには

**.hlkx** ファイルの作成とデジタル署名について詳しくは、[Windows HLK の概要](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)をご覧ください。

**.hckx** ファイルの作成とデジタル署名については、[Windows HCK の概要](https://go.microsoft.com/fwlink/p/?LinkId=248436)に関するページをご覧ください。

## <a name="to-submit-a-file"></a>ファイルを提出するには

1. パートナー センターにサインインし、**[Submit new hardware]\(新しいハードウェアの申請\)** を選択します。 これにより、提出を作成するためのウィザードが読み込まれます。

2. **[Packages and signing properties]** (パッケージと署名プロパティ) セクションで、ドライバー提出の名前を選びます。 この名前は、ドライバー提出の検索と整理に使うことができます。 注:別の会社とドライバーを共有する場合、この名前が表示されます。

3. 提出する **.hlkx/.hckx** ファイルをドラッグ アンド ドロップするか、参照します。 ファイルのアップロードが開始されます。
   ![ドライバー名フィールドを示すスクリーンショット](images/drivers-name.png)

4. この時点で、申請される製品の種類が申請ポータルによって確認されます。 その後、ポータルの申請ページに、Windows Server 認定用に申請された製品に関する必要な質問が表示されます。 Windows Server の認定や署名のために製品を申請し、申請ポータルに質問が表示された場合は、それらすべての製品について質問に回答する必要があります。 すべてに質問に回答するまで、申請は完了しません。

5. ドライバーをリリースする前にテストする場合は、[Perform test-signing for Win10 and above]\(Win10 以降のテスト署名を実行する\) または [Perform test-signing for OS below Win10 (legacy)]\(Win10 以前の OS (レガシー) のテスト署名を実行する\) チェック ボックスをオンにします。 テスト署名されたドライバーは、一般リリース用に署名されたドライバーとほぼ同じですが、HLK テストが不要です。 これらも Windows Update を通じて配布されず、ハードウェア提出サイトからダウンロードできます。 これらはテスト コンピューターにのみインストールできます。 ドライバー パッケージのテスト署名について詳しくは、「[WHQL Test Signature Program](https://docs.microsoft.com/windows-hardware/drivers/install/whql-test-signature-program)」 (WHQL テスト署名プログラム)と「[How to test-sign a driver package](https://docs.microsoft.com/windows-hardware/drivers/install/how-to-test-sign-a-driver-package)」 (ドライバー パッケージにテスト署名する方法) をご覧ください。

6. ドライバーをリリースする前にフライト署名する場合は、[Perform flight signing only]\(フライト署名のみ実行する\) チェック ボックスをオンにします。 フライト署名のドライバーは、すべての "Insider" ビルドによって信頼された Microsoft Developer Test 証明書を使用して署名されます。 製品版のシステムには、この証明書は使用されません。 フライト署名されたドライバーは、*Windows 10 Insider ビルド*にのみインストールできます。 つまり、Windows 10 の製品版ビルドに提供したり、インストールすることはできません。 フライト署名されたドライバーは、"セキュア ブート" が有効になった状態でのみ動作します。 フライト署名は Windows 10 RS2 以降にのみ適用でき、それ以前のバージョンの Windows では動作しません。 _この機能は現在、段階的にロールアウトされているため、すべてのユーザーに表示されるものではありません。表示されない場合は、表示されるまでお待ちください。数週間以内に表示されます。_

7. 必要に応じて、[署名を要求します] の項目を選択します。 このオプションでは、ドライバーに必要なオペレーティング システム署名 (適用可能な下位レベルのオペレーティング システムを含む) を指定できます。 利用可能な証明書はドライバー提出パッケージによって異なるため、一覧に表示されない証明書がある場合があります。 **注** 単一のアーキテクチャを対象としたドライバー パッケージに署名する場合は、対象となるアーキテクチャのログのみを含めてください。 たとえば、x64 専用のパッケージに署名する場合は、x64 のログのみを送信します。

   ![ドライバーの提出に使用できる証明書と、[Finalize] (最終処理) ボタンを示すスクリーンショット](images/additionalcertifications.png)

8. **[Certification]** (認定) セクションで、次の情報を入力します。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>フィールド</th>
   <th>説明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="even">
   <td><p>デバイスの種類</p></td>
   <td><p>デバイスが次のいずれかに該当するかどうかを示します。</p>
   <ul>
   <li><p>内部コンポーネント: システムの一部として PC 内部に接続されるデバイス。</p></li>
   <li><p>外部コンポーネント: PC に接続される外部デバイス (周辺機器)。</p></li>
   <li><p>その両方: 内部的に (PC 内で) 接続できるほか、外部的にも (周辺機器として) 接続できるデバイス。</p></li>
   </ul></td>
   </tr>
   <tr class="odd">
   <td><p>Device metadata category (デバイス メタデータ カテゴリ)</p></td>
   <td><p>デバイス カテゴリに基づく既定のアイコンのリストから、デバイスのアイコンを選びます。 この選択によって、[デバイスとプリンター] に表示されるアイコンが決まります。 デバイスが表示されないようにする場合は、[Internal device] (内部デバイス) を選びます。</p>
   <p>Windows Device Stage によるエクスペリエンスの向上については、「<a href="https://msdn.microsoft.com/library/windows/hardware/br230800.aspx" data-raw-source="[Device Metadata](https://msdn.microsoft.com/library/windows/hardware/br230800.aspx)">デバイス メタデータ</a>」をご覧ください。</p></td>
   </tr>
   <tr class="even">
   <td><p>Device metadata model ID (デバイス メタデータのモデル ID)</p></td>
   <td><p>それらの GUID は、従来の Sysdev ダッシュボードへのデバイス メタデータの提出を検証するために使われます。 指定した場合、デバイス メタデータ パッケージ内のモデル ID と一致する必要があります。</p></td>
   </tr>
   <tr class="odd">
   <td><p>Announcement date (発表日)</p></td>
   <td><p>Windows Server Catalog、Windows Certified Product List、ユニバーサル ドライバーの一覧に製品を含める日付を入力します。</p></td>
   </tr>
   <tr class="even">
   <td><p>Marketing names (マーケティング名)</p></td>
   <td><p>提出のマーケティング名を入力します。 マーケティング名には、製品のエイリアスを指定できます。 必要なだけ多くの名前を指定できます。</p></td>
   </tr>
   </tbody>
   </table>

   ![[Certification] (認定) セクションを示すスクリーンショット](images/drivers-certification.png)

9. **[送信]** を選びます。

10. **[Distribution]** (配布) セクションは、ドライバーを Windows Update に公開するために使います。 **[Distribution]** (配布) セクションの使用方法について詳しくは、「[出荷ラベルによるドライバーの配布の管理](manage-driver-distribution-by-submission.md)」をご覧ください。

11. ページ上部にある進行状況トラッカーで提出の進行状況を監視できます。 すべての手順が緑色のチェック マークになったら、提出が完了し、組織はダッシュボード ヘッダーに通知を受け取ります。

    ![進行状況トラッカーを示すスクリーンショット](images/drivers-allgreen-new.png)

12. 結果を確認します。 提出に失敗した場合は、必要な変更を加えて再提出してください。

## <a name="related-topics"></a>関連トピック

* [パートナー センターでハードウェア申請を管理する](manage-your-hardware-submissions.md)
* [複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
* [ドライバーのフライティング](driver-flighting.md)
