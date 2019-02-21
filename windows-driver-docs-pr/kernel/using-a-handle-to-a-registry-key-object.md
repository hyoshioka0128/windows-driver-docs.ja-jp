---
title: レジストリ キー オブジェクトを識別するハンドルを使用します。
description: レジストリ キー オブジェクトを識別するハンドルを使用します。
ms.assetid: 25982249-31dc-4542-9ebb-139991619b40
keywords:
- WDK カーネルのレジストリ キー オブジェクトへのハンドルします。
- レジストリ WDK カーネルでは、オブジェクトのルーチン
- ドライバーのレジストリ情報 WDK カーネル、オブジェクトのルーチン
- オブジェクトのルーチンの WDK カーネル
- レジストリ キー オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 558d905beb753e25bd380bbeb3d87aa672208370
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548743"
---
# <a name="using-a-handle-to-a-registry-key-object"></a>レジストリ キー オブジェクトを識別するハンドルを使用します。





次の表は、ドライバーは、適切なルーチンを呼び出すと、開いているキーで実行できる操作を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>呼び出すルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>キーを確認&#39;プロパティ、その名前またはそのサブキーの数などです。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567060" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567060)"><strong>ZwQueryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>キーを反復処理&#39;s サブキー、それぞれのプロパティを調べることです。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566447" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566447)"><strong>ZwEnumerateKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>値を含む、キー値のプロパティを調べる&#39;s データ。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567069" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567069)"><strong>ZwQueryValueKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>キーを反復処理&#39;s 値、それぞれのプロパティを調べることです。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566453" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566453)"><strong>ZwEnumerateValueKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>キーに関連付けられている値のデータを設定します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567109" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567109)"><strong>ZwSetValueKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>キーを削除します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566437" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566437)"><strong>ZwDeleteKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>キーの値を削除します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566439" data-raw-source="[&lt;strong&gt;ZwDeleteValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566439)"><strong>ZwDeleteValueKey</strong></a></p></td>
</tr>
</tbody>
</table>

 

呼び出す必要がありますが、ドライバーがその操作を完了すると[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)ハンドルを終了する — が既に呼び出されていない限り**ZwDeleteKey**キーを削除します。 (キーが削除されると、すべての開いているハンドルを無効になる、ので、ドライバーがここで、ハンドルを終了しないで必要があります。)

次のコード例は、という名前のキー ハンドルを開く方法を示しています**\\レジストリ\\マシン\\ソフトウェア\\**<em>MyCompany</em> 。\\*MyApp*、キーのデータを取得およびハンドルを終了します。

```cpp
//
// Get the frame location from the registry key
// HKLM\SOFTWARE\MyCompany\MyApp.
// For example: "FrameLocation"="X:\\MyApp\\Frames"
// 
HANDLE              handleRegKey = NULL;
for (int n = 0; n < 1; n++) 
{
    NTSTATUS           status = NULL;
    UNICODE_STRING     RegistryKeyName;
    OBJECT_ATTRIBUTES  ObjectAttributes;

    RtlInitUnicodeString(&RegistryKeyName, L"\\Registry\\Machine\\Software\\MyCompany\\MyApp");
    InitializeObjectAttributes(&ObjectAttributes, 
                               &RegistryKeyName,
                               OBJ_CASE_INSENSITIVE | OBJ_KERNEL_HANDLE,
                               NULL,    // handle
                               NULL);
    status = ZwOpenKey(&handleRegKey, KEY_READ, &ObjectAttributes);

    // If the driver cannot open the key, the driver cannot continue. 
    // In this situation, the driver was probably set up incorrectly 
    // and worst case, the driver cannot stream.
    if( NT_SUCCESS(status) == FALSE ) 
    {
        break;
    }
    // The driver obtained the registry key.
    PKEY_VALUE_FULL_INFORMATION  pKeyInfo = NULL;
    UNICODE_STRING               ValueName;
    ULONG                        ulKeyInfoSize = 0;
    ULONG                        ulKeyInfoSizeNeeded = 0;

    // The driver requires the following value.
    RtlInitUnicodeString(&ValueName, L"FrameLocation");

    // Determine the required size of keyInfo.
    status = ZwQueryValueKey( handleRegKey,
                              &ValueName,
                              KeyValueFullInformation,
                              pKeyInfo,
                              ulKeyInfoSize,
                              &ulKeyInfoSizeNeeded );

    // The driver expects one of the following errors.
    if( (status == STATUS_BUFFER_TOO_SMALL) || (status == STATUS_BUFFER_OVERFLOW) )
    {
        // Allocate the memory required for the key.
        ulKeyInfoSize = ulKeyInfoSizeNeeded;
        pKeyInfo = (PKEY_VALUE_FULL_INFORMATION) ExAllocatePoolWithTag( NonPagedPool, ulKeyInfoSizeNeeded, g_ulTag);
        if( NULL == pKeyInfo )
        {
            break;
        }
        RtlZeroMemory( pKeyInfo, ulKeyInfoSize );

        // Get the key data.
        status = ZwQueryValueKey( handleRegKey,
                                  &ValueName,
                                  KeyValueFullInformation,
                                  pKeyInfo,
                                  ulKeyInfoSize,
                                  &ulKeyInfoSizeNeeded );
        if( (status != STATUS_SUCCESS) || (ulKeyInfoSizeNeeded != ulKeyInfoSize) || (NULL == pKeyInfo) )
        {
            break;
        }

        // Fill in the frame location if it has not been filled in already.
        if ( NULL == m_szwFramePath )
        {
            m_ulFramePathLength = pKeyInfo->DataLength;
            ULONG_PTR   pSrc = NULL;

            pSrc = (ULONG_PTR) ( (PBYTE) pKeyInfo + pKeyInfo->DataOffset);

            m_szwFramePath = (LPWSTR) ExAllocatePoolWithTag( NonPagedPool, m_ulFramePathLength, g_ulTag);
            if ( NULL == m_szwFramePath )
            {
                m_ulFramePathLength = 0;
                break;
            }

            // Copy the frame path.
            RtlCopyMemory(m_szwFramePath, (PVOID) pSrc, m_ulFramePathLength);
        }
        // The driver is done with the pKeyInfo.
        xFreePoolWithTag(pKeyInfo, g_ulTag);

    } // if( (status == STATUS_BUFFER_TOO_SMALL) || (status == STATUS_BUFFER_OVERFLOW) )
} // Get the Frame location from the registry key.

// All done with the registry.
if (NULL != handleRegKey)
{
    ZwClose(handleRegKey);
}
```

システムでは、メモリ内のキーの変更をキャッシュし、数秒ごとのディスクに書き込みます。 ディスクに、キーの変更を強制的に[ **ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)します。

シンプルなインターフェイス経由でのレジストリを操作するドライバーを呼び出すことも、 **Rtl*Xxx*レジストリ * Xxx*** ルーチン。 詳細については、次を参照してください。[レジストリ ランタイム ライブラリ ルーチン](registry-run-time-library-routines.md)します。

 

 




