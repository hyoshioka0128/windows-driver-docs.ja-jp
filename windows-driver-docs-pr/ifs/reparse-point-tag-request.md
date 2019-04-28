---
title: 再解析ポイント タグ要求
description: これは、いずれかの必要があるこれらのファイル システム フィルター ドライバーの再解析ポイント タグを取得するためのメカニズムです。
ms.assetid: B4E4382B-4FB8-4E21-8FC4-EDDE8DD4AC77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed9aa4f44f08bd41a64588d5f8350074dfc2b7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370108"
---
# <a name="reparse-point-tag-request"></a>再解析ポイント タグ要求


これは、いずれかの必要があるこれらのファイル システム フィルター ドライバーの再解析ポイント タグを取得するためのメカニズムです。

## <a name="span-idreparsepointtagrequestspanspan-idreparsepointtagrequestspanspan-idreparsepointtagrequestspanreparse-point-tag-request"></a><span id="Reparse_Point_Tag_Request"></span><span id="reparse_point_tag_request"></span><span id="REPARSE_POINT_TAG_REQUEST"></span>ポイント タグの要求を再解析します。


再解析ポイント タグを取得するには、次の情報をマイクロソフトに送信します。

-   会社名
-   会社の電子メール
-   会社の URL
-   連絡先の電子メール
-   製品名
-   製品の URL
-   製品の説明:(1 段落の概要)
-   ドライバーのファイル名
-   ドライバーのデバイス名
-   ドライバーの GUID
-   (はい/いいえ) を有効になっている待機時間の長いビット
-   (はい/いいえ) を有効になっている名前サロゲート ビット

この情報を送信する ASCII テキスト電子メール メッセージで<rpid@microsoft.com>します。 A *ReparseID*このドライバーは、指定した連絡先の電子メール アドレスに電子メールで送信されることの値します。

次の一覧では、要求を送信するためのいくつかの要件について説明します。

- すべてのフィールドに入力する必要があります。

- ユーザーにとってこの公開されている表示可能なデータベースで、独自の名前と電子メール アドレスを使用したくない、このような使用の電子メール アドレスを作成します (ファイル システム/フィルター ドライバーが含まれている製品があるその他の企業が相互運用性に問題があります。自分が作成、して互いに通信する 2 つの会社のテスト/開発チームを取得する必要が)。 推奨される名前は *"ntifskit@YourCompanyName.com"* します。

- 「高待機時間」のビットが有効になっている場合このドライバーのタグ ファイルを意味し、待ち時間が長いが付与されます。 たとえば、ドライバーには階層のストレージ ソリューションなどを実装するために再解析ポイントを使用してこの設定は。

- つまり「名サロゲート」ビットが有効になっている場合は、ドライバーがシステム内の別の名前付きエンティティを表します。 たとえば、またはディレクトリの分岐点のボリュームのマウント ポイントの名前です。

- 再解析ポイントは、Windows の強力な機能が、開発者は、1 ファイル再解析ポイントを 1 つしか存在できません、Windows のいくつかのメカニズムを使用して、再解析ポイント (HSM、ネイティブの構造化ストレージ) 必要があります。 開発者は、ファイルを使用して、再解析ポイント タグが既にがのフォールバック ストラテジが必要です。

 

 




