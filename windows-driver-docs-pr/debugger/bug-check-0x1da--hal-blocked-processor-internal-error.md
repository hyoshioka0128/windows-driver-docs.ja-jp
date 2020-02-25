---
title: バグチェック 1DA HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
description: HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR の値は0x000001DA です。
keywords:
- バグチェック 0x1DA HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
- HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
ms.date: 02/20/2020
topic_type:
- apiref
api_name:
- HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a251cb9ce152aaf974d231fe519db718e20b55e9
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77530336"
---
# <a name="bug-check-0x1da-hal_blocked_processor_internal_error"></a>バグチェック 0x1DA: HAL\_ブロックされている\_プロセッサ\_内部\_エラー

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

\_ブロックされている HAL\_プロセッサ\_内部\_エラーの値は0x000001DA です。 これは、ブロックされたプロセッサライブラリで内部エラーが検出されたことを示します。

## <a name="hal_blocked_processor_internal_error-parameters"></a>HAL\_ブロックされている\_プロセッサ\_内部\_エラーパラメーター

次のパラメーターがブルースクリーンに表示されます。

| パラメーター |                        説明              |
|-----------|-------------------------------------------------|
|     1     | エラーの種類-以下を参照してください                     |
|     2     | 以下をご覧ください。                                      |
|     3     | 以下をご覧ください。                                      |
|     4     | 以下をご覧ください。                                      |

## <a name="parameter-one-values"></a>パラメーター1の値

```plaintext
            0x01 : Library initialization failure
                2 - NT status code
            0x02 : Processor start failure
                2 - Processor index
                3 - APIC ID
            0x03 : PPM package ID query failure
                2 - Processor index
            0x04 : PPM operation failure
                2 - Operation
                    0x01 : MSR read
                    0x02 : MSR write
                    0x03 : I/O port read
                    0x04 : I/O port write
                    0x05 : Idle state registration
                3 - Processor index
                4 - PPM mailbox
            0x05 : A blocked processor has encountered a fatal exception.
                2 - Processor index
                3 - Vector number
                4 - Trap frame
            0x06 : PPM operation timeout
                2 - Operation
                    0x01 : MSR read
                    0x02 : MSR write
                    0x03 : I/O port read
                    0x04 : I/O port write
                    0x05 : Idle state registration
                3 - Processor index
                4 - PPM mailbox
```
