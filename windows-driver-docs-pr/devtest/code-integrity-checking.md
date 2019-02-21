---
title: コードの整合性チェック
description: Driver Verifier のコードの整合性チェック
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- Driver Verifier のコードの整合性チェック
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a1d3584df9d82f19f22716d405658c2340b011
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536947"
---
# <a name="code-integrity-checking"></a>コードの整合性チェック

[Device Guard](https://blogs.msdn.microsoft.com/windows_hardware_certification/2015/05/22/driver-compatibility-with-device-guard-in-windows-10/) Windows オペレーティング システムの残りの部分からコードの整合性 (CI) の意思決定関数を分離するハードウェア テクノロジと仮想化を使用できます。 仮想化ベースのセキュリティを使用して、コードの整合性を分離する、カーネル メモリは、実行可能になることができますのみの方法は、コードの整合性の検証です。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。 コードの整合性チェックでは、これらのコードの整合性規則の互換性を確保し、次の違反を検出します。

<table>
  <tr>
    <th>エラー コード</th>
    <th>コードの整合性の問題</th>
  </tr>
  <tr>
    <td>0x2000:
        <ul>
            <li>2 ドライバーでは、-アドレス&#39;コード、エラーが検出されました。</li>
            <li>3-プールの種類。</li>
            <li>4-プール タグ (存在する場合)。</li>
        </ul><br/>    </td>
    <td>呼び出し元は、プールの実行可能ファイルの種類を指定します。 (想定します。NonPagedPoolNx)</td>
  </tr>
  <tr>
    <td>0x2001:
        <ul><li>2 ドライバーでは、-アドレス&#39;コード、エラーが検出されました。</li>
        <li>3-ページ保護 (WIN32_PROTECTION_MASK)。
    </td>
    <td>呼び出し元は、実行可能ファイルのページ保護を指定します。 (Expected: cleared PAGE_EXECUTE* bits)</td>
  </tr>
  <tr>
    <td>0x2002 の場合:
        <ul><li>2 ドライバーでは、-アドレス&#39;コード、エラーが検出されました。</li>
            <li>3-ページ優先順位 (MM_PAGE_PRIORITY 論理的にまたは&#39;d MdlMapping *)。</li></ul>
    </td>
    <td>呼び出し元は、実行可能ファイルの MDL マッピングを指定します。 (想定します。MdlMappingNoExecute)。</td>
  </tr>
  <tr>
    <td>0x2003:
        <ul><li>2 - イメージ ファイル名 (Unicode 文字列)。</li>
            <li>3 - セクション ヘッダーのアドレス。</li>
            <li>4-セクション名 (utf-8 でエンコードされた文字列)。</li></ul>
    </td>
    <td>イメージには、実行可能ファイル/書き込み可能なセクションが含まれています。</td>
  </tr>
  <tr>
    <td>0x2004:
        <ul><li>2 - イメージ ファイル名 (Unicode 文字列)。</li>
            <li>3 - セクション ヘッダーのアドレス。</li>
            <li>4-セクション名 (utf-8 でエンコードされた文字列)。</li></ul>
    </td>
    <td>イメージには、ページに合わせるないセクションが含まれています。</td>
  </tr>
  <tr>
    <td>0x2005:
        <ul><li>2 - イメージ ファイル名 (Unicode 文字列)。</li>
            <li>3-IAT ディレクトリ。</li>
            <li>4-セクション名 (utf-8 でエンコードされた文字列)。</li><ul>
    </td>
    <td>イメージには、実行可能ファイルのセクションにある、IAT が含まれています。</td>
  </tr>
</table>

### <a name="activating-this-option"></a>このオプションをアクティブ化。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーを確認するポート/ミニポート インターフェイスを有効にすることができます。 詳細については、次を参照してください。 [driver verifier のオプションを選択する](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)します。 オプションをオンにするポート/ミニポート インターフェイスをアクティブ化またはコンピューターを再起動する必要があります。

* **コマンドラインで**

    、コマンドラインでポート ミニポート インターフェイスのチェックで表される**0x02000000 (ビット 25)** します。 次に、例を示します。

    `verifier /flags 0x02000000 /driver MyDriver.sys`

    この機能は、[次へ] の起動後にアクティブになります。

* **ドライバー検証マネージャーを使用します。**

1. ドライバー検証マネージャーを起動します。 コマンド プロンプト ウィンドウで、検証方法を入力します。
2. (コードの開発者) の作成のカスタム設定を選択し、[次へ] をクリックします。
3. Select(check) ポート ミニポート インターフェイスをチェックします。
4. コンピューターを再起動します。
