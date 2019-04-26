---
title: セキュリティ
description: Windows 10 Mobile のセキュリティについての詳細はこのセクションのトピックを使用します。
ms.assetid: 15783e59-f37b-4373-8604-d35c57eedfcc
ms.date: 08/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13a35de780c5165bdd4b336dc1e3e4d879394529
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337521"
---
# <a name="security"></a>セキュリティ

Windows 10 のセキュリティについて説明します。

## <a name="os-security-tasks"></a>OS セキュリティ タスク

セキュリティで保護されたデバイスを作成するには、OEM は次のタスクを実行する必要があります。

<table>
  <thead>
    <th>タスク</th>
    <th>説明</th>
  </thead>
  <tbody>
    <tr>
      <td>さまざまな種類の実行可能コードとその他のコード資産に署名する方法について説明します</td>
      <td>すべての Windows 10 Mobile のバイナリには、デジタル署名の読み込みおよび小売スマート フォンで実行する必要があります。 For more info, see:<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate">コード署名証明書を入手して</a>します。</td>
</tr>
<tr class="even">
<td>イメージの検証と暗号化を理解します。</td>
<td>Windows 10 Mobile を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot">セキュリティで保護された boot</a>、実行を許可する前に、ファームウェア イメージを検証するプロセス。 Windows 10 Mobile も用意されています。<a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot-and-device-encryption-overview">デバイスの暗号化</a>、内部データのパーティションに格納されているすべてのユーザー データを暗号化する機能。 Oem は、これらの機能を有効にする製造時に、一連のタスクを実行する必要があります。</td>
</tr>
<tr>
<td>Security Development Lifecycle (SDL) を理解します。</td>
<td><a href="https://www.microsoft.com/sdl">Security Development Lifecycle (SDL)</a>ベスト プラクティスと関連付けられているツールは自社製品のセキュリティ強化のための Oem によって使用できます。</td>
</tr>
</tbody>
</table>

## <a name="sdl-recommendations-for-oems"></a>Oem の SDL の推奨事項

Microsoft Security Development Lifecycle (SDL) は、一連のベスト プラクティスと Oem は自社製品のセキュリティを向上させるために使用して関連するツールです。 SDL のプラクティスには最も効果的な従来のソフトウェア開発ライフ サイクルの段階で整理されます。 たとえば、脅威のモデル化は、ソフトウェア設計時に最も有効です。

ある程度のセキュリティ上の利点は、スタンドアロンごとに実装されている場合、これらのセキュリティ活動多く提供はします。 ただし、Microsoft で実際の経験が示されてよりも反復可能なプロセスの一部として、ソフトウェア開発ライフ サイクルの適切なフェーズ中に、時系列順で実行されるアクティビティは、セキュリティを強化されることがセキュリティを取得します。アドホック実装に起因します。 SDL の詳細については、次を参照してください。 [Microsoft セキュリティ開発ライフ サイクル](https://www.microsoft.com/sdl)します。

次の表では、SDL のプラクティスを採用する OEM に最も適しているのサブセットについて説明します。 これらのプラクティスのいくつかは、他のユーザーはアプリケーション コードをより便利なドライバーのコードによりに役立ちます。 SDL のプラクティスをいくつかは、両方に役立ちます。 ドライバーは、ドライバーのコードを開発するときに、これらのベスト プラクティスを考慮することが重要であるためより高い特権で実行する傾向があります。

|ツール|情報|推奨される領域|
|----|----|----|
|[Microsoft SDL Threat Modeling Tool](https://www.microsoft.com/download/details.aspx?id=49168)|SDL Threat Modeling Tool は、設計者および開発者、システムの脅威モデルを作成し、潜在的なセキュリティの問題、システムの設計での脅威モデルを分析できます。 脅威のモデル化は、デザインが完了する前にデザイン時に最も有効です。 詳細については、次を参照してください。 [SDL 実習 7: 脅威のモデル化を使用して、](https://www.microsoft.com/sdl/process/design.aspx)します。|Driver (ドライバー)|
|[FxCop](https://www.microsoft.com/SDL/adopt/tools.aspx)|FxCop では、静的アナライザーです。 マネージ コード アセンブリを分析し、可能なデザイン、ローカリゼーション、パフォーマンス、およびセキュリティの強化など、アセンブリに関する情報を報告します。|パートナーのアプリ|
|[FxCop コード分析から .NET コンパイラ プラットフォームのアナライザーへの移行します。](https://docs.microsoft.com/visualstudio/code-quality/fxcop-analyzers)|Visual Studio 2017 には、一連組み込みを入力すると、c# または Visual Basic のコードを分析する .NET コンパイラ プラットフォームのアナライザーにはが含まれています。 NuGet パッケージとして、Visual Studio 拡張機能として、またはプロジェクトごとにその他のアナライザーをインストールできます。 アナライザーは、コード スタイル、コードの品質と保守容易性、コードの設計、およびその他の問題を確認します。|マネージ コードでのパートナーのアプリ|
|[BinSkim](https://www.microsoft.com/SDL/adopt/tools.aspx)|BinSkim は、Windows ポータブル実行可能ファイル (PE) ファイルのセキュリティと正確性をスキャンするバイナリの静的分析ツールです。  BinSkim によって実行される検証は、すべての Windows プラットフォームによって提供されるバイナリの軽減策を選択した PE ファイルを検証します。 ([ユーザー ガイド](https://github.com/Microsoft/binskim/blob/develop/docs/BinSkimUserGuide.docx))|ドライバーとパートナーのアプリ|
|[C/C++ のコード分析](https://docs.microsoft.com/visualstudio/code-quality/code-analysis-for-c-cpp-overview)|C/C++ 用のコード分析は、Visual Studio Team System Development Edition のインストールで提供される静的アナライザーまたは、コード障害を検出および修正するには、Visual Studio Team Suite と役立ちます。 一度にでは、ソース コードの 1 つの関数を plows し、C と C++ のコーディング パターンとプログラミング エラーを示す可能性のある不適切なコードの使用状況を検索します。|ドライバーとパートナーのアプリ|
