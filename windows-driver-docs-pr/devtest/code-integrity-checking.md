---
title: コードの整合性チェック
description: ドライバーの検証ツールのコードの整合性チェック
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- ドライバーの検証ツールのコードの整合性チェック
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0dad7dd96c1d84d3f3591615fb55ca543264954
ms.sourcegitcommit: 46b135fe70134bba6cbb8111ce0def7100eed027
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82973285"
---
# <a name="code-integrity-checking"></a>コード整合性チェック

[ハイパーバイザーで保護されたコードの整合性](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/use-device-guard-readiness-tool)では、ハードウェアテクノロジと仮想化を使用して、コード整合性 (CI) の意思決定機能を Windows オペレーティングシステムの他の部分から分離できます。 仮想化ベースのセキュリティを使用してコードの整合性を分離する場合、カーネルメモリを実行可能ファイルにする唯一の方法は、コードの整合性を検証することです。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。 コードの整合性チェックによって、これらのコード整合性規則の互換性が確保され、次の違反が検出されます。

<table>
  <tr>
    <th>エラー コード</th>
    <th>コードの整合性の問題</th>
  </tr>
  <tr>
    <td>0x2000
        <ul>
            <li>2-ドライバーのコード内でエラーが検出されたアドレス。</li>
            <li>3-プールの種類。</li>
            <li>4-プールタグ (指定されている場合)。</li>
        </ul><br/>    </td>
    <td>呼び出し元は、実行可能なプールの種類を指定しました。 (必要な値: NonPagedPoolNx)</td>
  </tr>
  <tr>
    <td>0x2001:
        <ul><li>2-ドライバーのコード内でエラーが検出されたアドレス。</li>
        <li>3-ページ保護 (WIN32_PROTECTION_MASK)。
    </td>
    <td>呼び出し元は、実行可能ページの保護を指定しました。 (必要なのは、消去された PAGE_EXECUTE * ビット)</td>
  </tr>
  <tr>
    <td>0x2002
        <ul><li>2-ドライバーのコード内でエラーが検出されたアドレス。</li>
            <li>3-ページの優先度 (MM_PAGE_PRIORITY、MdlMapping *)。</li></ul>
    </td>
    <td>呼び出し元は、実行可能な MDL マッピングを指定しました。 (必要な値: MdlMappingNoExecute)。</td>
  </tr>
  <tr>
    <td>0x2003:
        <ul><li>2-イメージファイル名 (Unicode 文字列)。</li>
            <li>3-セクションヘッダーのアドレス。</li>
            <li>4-セクション名 (UTF-8 でエンコードされた文字列)。</li></ul>
    </td>
    <td>イメージには、実行可能ファイルと書き込み可能セクションが含まれています。</td>
  </tr>
  <tr>
    <td>0x2004:
        <ul><li>2-イメージファイル名 (Unicode 文字列)。</li>
            <li>3-セクションヘッダーのアドレス。</li>
            <li>4-セクション名 (UTF-8 でエンコードされた文字列)。</li></ul>
    </td>
    <td>このイメージには、ページがアラインされていないセクションが含まれています。</td>
  </tr>
  <tr>
    <td>0x2005:
        <ul><li>2-イメージファイル名 (Unicode 文字列)。</li>
            <li>3-IAT ディレクトリ。</li>
            <li>4-セクション名 (UTF-8 でエンコードされた文字列)。</li><ul>
    </td>
    <td>イメージには、実行可能なセクションに配置されている IAT が含まれています。</td>
  </tr>
</table>

### <a name="activating-this-option"></a>このオプションをアクティブにする:

Driver Verifier マネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーのコードの整合性チェックをアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)」を参照してください。 コードの整合性チェックオプションをアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。

* **コマンドラインで**

    コマンドラインでは、コードの整合性チェックは**0x02000000 (ビット 25)** によって表されます。 次に例を示します。

    `verifier /flags 0x02000000 /driver MyDriver.sys`

    この機能は、次回の起動時にアクティブになります。

* **ドライバー検証マネージャーの使用**

1. ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「Verifier」と入力します。
2. [カスタム設定の作成] (コード開発者向け) を選択し、[次へ] をクリックします。
3. コードの整合性チェックを選択 (チェック) します。
4. コンピューターを再起動します。

## <a name="related-topics"></a>関連トピック

[HVCI ドライバーの互換性を評価する](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/use-device-guard-readiness-tool)
