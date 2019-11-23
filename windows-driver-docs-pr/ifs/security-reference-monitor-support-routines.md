---
title: セキュリティリファレンスモニタのサポートルーチン
description: セキュリティリファレンスモニタのサポートルーチン
ms.assetid: 56cb152b-7c98-48ed-8fe9-72351588e440
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 269e90618d8943e86bc812c05d1484130c98a5bc
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955782"
---
# <a name="security-reference-monitor-support-routines"></a>セキュリティリファレンスモニタのサポートルーチン

次の表は、システムによって提供されるセキュリティリファレンスサポートルーチンのうち、カーネルモードのファイルシステムで使用できるものと、ミニフィルターとレガシフィルタードライバーによって使用されるものの、デバイスドライバーによるものではないものを示しています。

ここに記載されているルーチンに加えて、ファイルシステムとフィルタードライバーは、 *ntifs*で宣言されているカーネルモードドライバーアーキテクチャリファレンスセクションで説明されているすべての**Se**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

**プレフィックス: Se**_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **SeAppendPrivileges** | アクセス状態構造の特権セットに追加の特権を追加します。 |
| **Seaudith/リンクの作成** | システム用に予約されています。 |
| **SeAuditingFileEvents** | ファイルオープンイベントが現在監査されているかどうかを判断します。 |
| **SeAuditingFileOrGlobalEvents** | ファイルまたはグローバルイベントが現在監査されているかどうかを判断します。 |
| **SeAuditingHardLinkEvents** | システム用に予約されています。 |
| **Secapの Subjectsubjectcontext** | アクセス検証と監査のために、呼び出し元スレッドのセキュリティコンテキストをキャプチャします。 |
| **SeCreateClientSecurity** | **SeImpersonateClientEx**を呼び出すために必要な情報を使用して、セキュリティクライアントのコンテキスト構造を初期化します。 |
| **SeCreateClientSecurityFromSubjectContext** | セキュリティサブジェクトコンテキストのアクセストークンを取得し、その結果を使用して、 **SeImpersonateClientEx**を呼び出すために必要な情報を使用してセキュリティクライアントコンテキストを初期化します。 |
| **SeDeleteClientSecurity** | クライアントのセキュリティコンテキストを削除します。 |
| **SeDeleteObjectAuditAlarm** | 削除対象としてマークされているオブジェクトの監査メッセージとアラームメッセージを生成します。 |
| **SeFilterToken** | 既存のアクセストークンの制限付きバージョンである新しいアクセストークンを作成します。 |
| **SeImpersonateClient** | 使われていません。 |
| **SeImpersonateClientEx** | スレッドがユーザーの権限を借用します。 |
| **SeLengthSid** | 使われていません。 |
| **SeLockSubjectContext** | キャプチャされたサブジェクトコンテキストのプライマリトークンと偽装トークンをロックします。 |
| **SeMarkLogonSessionForTerminationNotification** | ログオンセッションが終了したときに、呼び出し元の登録済みコールバックルーチンが呼び出されるように、ログオンセッションをマークします。 ログオンセッションは、ログオンセッションを参照している最後のトークンが削除されると終了します。 |
| **SeOpenObjectAuditAlarm** | オブジェクトを開こうとしたときに、監査メッセージとアラームメッセージを生成します。 |
| **SeOpenObjectForDeleteAuditAlarm** | オブジェクトを削除対象として開こうとしたときに、監査メッセージとアラームメッセージを生成します。 |
| **SePrivilegeCheck** | サブジェクトのアクセストークンで、指定された特権のセットが有効かどうかを判断します。 |
| **SeQueryAuthenticationIdToken** | アクセストークンの認証 ID を取得します。 |
| **SeQueryInformationToken** | アクセストークンに関する指定された種類の情報を取得します。 呼び出しプロセスは、情報を取得するための適切なアクセス権を持っている必要があります。 |
| **Sequerysecurity記述子情報** | オブジェクトのセキュリティ記述子のコピーを取得します。 |
| **SeQuerySessionIdToken** | システム用に予約されています。 |
| **SeQuerySubjectContextToken** | セキュリティサブジェクトコンテキストのアクセストークンを取得します。 |
| **SeRegisterLogonSessionTerminatedRoutine** | ログオンセッションが終了したときに呼び出されるコールバックルーチンを登録します。 ログオンセッションは、ログオンセッションを参照している最後のトークンが削除されると終了します。 |
| **SeReleaseSubjectContext** | 以前の**Secapturesubjectcontext**の呼び出しによってキャプチャされたサブジェクトセキュリティコンテキストを解放します。 |
| **SeSetAccessStateGenericMapping** | ACCESS_STATE 構造体の汎用マッピングフィールドを設定します。 |
| **Sesetsecurity記述子情報** | オブジェクトのセキュリティ記述子を設定します。 |
| **Sesetsecurity記述子 Infoex** | オブジェクトのセキュリティ記述子を変更し、オブジェクトがアクセス制御エントリ (ACE) の自動継承をサポートするかどうかを指定します。 |
| **SeSetSessionIdToken** | システム用に予約されています。 |
| **SeStopImpersonatingClient** | 呼び出し元のスレッドのユーザーの偽装を終了します。 |
| **SeTokenIsAdmin** | トークンにローカルの administrators グループが含まれているかどうかを判断します。 |
| **SeTokenIsRestricted** | トークンに制限のあるセキュリティ識別子 (SID) の一覧が含まれているかどうかを判断します。 |
| **SeTokenType** | システム用に予約されています。 |
| **SeUnlockSubjectContext** | **Selocksubjectcontext**への呼び出しによってロックされていた、キャプチャされたサブジェクトコンテキストのトークンのロックを解除します。 |
| **SeUnregisterLogonSessionTerminatedRoutine** | 以前の**SeRegisterLogonSessionTerminatedRoutine**の呼び出しで登録されたコールバックルーチンの登録を解除します。 |
