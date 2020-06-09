---
title: バグチェック 0x149 REFS_FILE_SYSTEM
description: REFS_FILE_SYSTEM のバグチェックの値は0x00000149 です。 これは、ファイルシステムエラーが発生したことを示します。
ms.assetid: 899E89E7-46CD-4143-B1DC-7959F01643CF
keywords:
- バグチェック 0x149 REFS_FILE_SYSTEM
- REFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6e36636600ee91523922e92dfedc6791c9aaf3e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534843"
---
# <a name="bug-check-0x149-refs_file_system"></a>バグチェック 0x149: REFS \_ ファイル \_ システム


REFS \_ ファイル \_ システムのバグチェックの値は0x00000149 です。 これは、ファイルシステムエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="refs_file_system-parameters"></a>REFS \_ ファイル \_ システムパラメーター


| パラメーター | 説明                          |
|-----------|--------------------------------------|
| 1         | \_\_直線\_\_                         |
| 2         | ExceptionRecord                      |
| 3         | ContextRecord                        |
| 4         | ExceptionRecord- &gt; exceptionrecord |

 

| パラメーター | 説明 |
|-----------|-------------|
| 1         | Message     |
| 2         | 予約済み    |
| 3         | 予約済み    |
| 4         | 予約済み    |

 

<a name="resolution"></a>解像度
----------

スタックに RefsExceptionFilter が表示された場合、2番目と3番目のパラメーターは例外レコードとコンテキストレコードになります。 2番目のパラメーターで[**. exr**](-exr--display-exception-record-.md)を実行して例外情報を表示し、3番目のパラメーターでは[**cxr**](-cxr--display-context-record-.md)を実行し、より有益なスタックトレースを取得するには[**kb**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)を実行します。

 

 




