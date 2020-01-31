---
title: 再解析ポイント タグ要求
description: これは、再解析ポイントタグを取得するためのメカニズムです。このタグは、必要なファイルシステムフィルタドライバー用です。
ms.assetid: B4E4382B-4FB8-4E21-8FC4-EDDE8DD4AC77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 229d74ba266c22da7369ad5eef5c39764b5c7e0d
ms.sourcegitcommit: 6997fcbd0ad57e189c4b7c6b490632d1d53b6b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822818"
---
# <a name="reparse-point-tag-request"></a>再解析ポイント タグ要求


これは、再解析ポイントタグを取得するためのメカニズムです。このタグは、必要なファイルシステムフィルタドライバー用です。

## <a name="span-idreparse_point_tag_requestspanspan-idreparse_point_tag_requestspanspan-idreparse_point_tag_requestspanreparse-point-tag-request"></a><span id="Reparse_Point_Tag_Request"></span><span id="reparse_point_tag_request"></span><span id="REPARSE_POINT_TAG_REQUEST"></span>再解析ポイントタグ要求


再解析ポイントタグを取得するには、次の情報を Microsoft に送信します。

-   会社名
-   会社の電子メール
-   会社の URL
-   連絡先の電子メール
-   製品名です
-   製品の URL
-   製品の説明: (1 段落の概要)
-   ドライバーのファイル名
-   ドライバーデバイス名
-   ドライバー GUID
-   待機時間が長いビットを有効にする (はい/いいえ)
-   名前サロゲートビット有効 (はい/いいえ)

この情報を ASCII テキストの電子メールメッセージで <rpid@microsoft.com>に送信します。 このドライバーの*ReparseID*値は、指定された連絡先の電子メールアドレスに電子メールで送信されます。

次の一覧では、要求を送信するためのいくつかの要件について説明します。

- すべてのフィールドに入力する必要があります。

- この一般公開されているデータベースで独自の名前と電子メールアドレスを使用したくない場合は、この使用のための電子メールアドレスを作成してください (お客様の相互運用性の問題がある、ファイルシステム/フィルタードライバーを含む製品がある他の企業にとって、相互に通信するために2社の企業のテスト/開発 推奨される名前は *"ntifskit@YourCompanyName.com"* です。

- "高待機時間" ビットが有効になっている場合は、ドライバーがファイルにタグを付け、待機時間が長いことが予想されます。 たとえば、これは、再解析ポイントを使用して階層型ストレージソリューションを実装するドライバーによって設定されます。

- "Name サロゲート" ビットが有効になっている場合、ドライバーはシステム内の別の名前付きエンティティを表すことを意味します。 たとえば、ボリュームマウントポイントの名前、またはディレクトリジャンクションの名前などです。

- 再解析ポイントは Windows の強力な機能ですが、開発者はファイルごとに1つの再解析ポイントしか存在できず、一部の Windows メカニズムでは再解析ポイント (HSM、ネイティブ構造化ストレージ) が使用されていることに注意する必要があります。 開発者は、再解析ポイントタグがファイルに対して既に使用されている場合のフォールバックストラテジを持っている必要があります。

 

 




