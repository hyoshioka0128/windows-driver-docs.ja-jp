---
title: プロセス構造のサポートルーチン
description: プロセス構造のサポートルーチン
ms.assetid: 2cf3ab25-9db8-4a20-982d-eda0c3c96dbc
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: ebc1def03cc42ee5f59a618556053e0fdc8a7ae0
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955826"
---
# <a name="process-structure-support-routines"></a>プロセス構造のサポートルーチン

次の表に、カーネルモードのファイルシステムおよびミニフィルターとレガシフィルタードライバーで使用できるシステム指定のプロセス構造サポートルーチンのサブセットを示します。 これらのルーチンは、デバイスドライバーでは使用できません。

ここに記載されているルーチンに加えて、ファイルシステムとフィルタードライバーは、「カーネルモードドライバーアーキテクチャリファレンス」セクションで説明されている、 *ntifs*で宣言されている**Ps**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

**プレフィックス: Ps**_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **PsChargePoolQuota** | 指定されたプロセスに対して、指定されたプールの種類の課金プールのクォータを指定します。 |
| **PsDereferenceImpersonationToken** | 偽装トークンの参照カウントをデクリメントします。 |
| **PsDereferencePrimaryToken** | プライマリトークンの参照カウントをデクリメントします。 |
| **PsIsDiskCountersEnabled** | プロセスごとのディスク i/o カウンターの有効な状態を返します。 |
| **PsGetProcessExitTime** | 現在のプロセスの終了時刻を返します。 |
| **クライアントを** | サーバースレッドがクライアントを偽装するようにします。 |
| **PsIsThreadTerminating** | スレッドが終了しているかどうかを確認します。 |
| **PsLookupProcessByProcessId** | プロセスのプロセス ID を受け取り、プロセスの EPROCESS 構造への参照先ポインターを返します。 |
| **PsLookupThreadByThreadId** | スレッドのスレッド ID を受け取り、そのスレッドの ETHREAD 構造体への参照されたポインターを返します。 |
| **PsReferenceImpersonationToken** | 指定したスレッドの偽装トークンの参照カウントをインクリメントします。 |
| **PsReferencePrimaryToken** | 指定されたプロセスのプライマリトークンの参照カウントをインクリメントします。 |
| **PsReturnPoolQuota** | 指定されたプールの種類のプールクォータを、指定されたプロセスに返します。 |
| **PsRevertToSelf** | 呼び出し元スレッドのクライアントの偽装を終了します。 |
| **PsUpdateDiskCounters** | 指定されたプロセスのディスク i/o カウンターを更新します。 |
