---
title: 移植に関する問題のチェックリスト
description: 移植に関する問題のチェックリスト
ms.assetid: 6ab26321-85b8-4a5b-8ca5-af6cbf56ccd6
keywords:
- 64-bit WDK カーネル、移植 (ドライバーを)
- 64ビット版 Windows へのドライバーの移植
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e523c95115c6994216d83bf8d9dbffe89e649487
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827662"
---
# <a name="porting-issues-checklist"></a>移植に関する問題のチェックリスト





### <a name="general"></a>[全般]

-   新しい64ビットセーフな Windows データ型を使用します。

    このドキュメントで既に説明した新しい64ビットセーフデータ型は、Basetsd で定義されています。 このヘッダーファイルは、Ntddk、Wdm、および Ntifs に含まれる Ntdef. h に含まれています。

-   Platform compiler マクロは慎重に使用してください。

    次の前提条件が無効になりました。

    ```cpp
    #ifdef _WIN32  // 32-bit Windows code
    ...
    #else          // 16-bit Windows code
    ...
    #endif
    ```

    ただし、64ビットコンパイラでは、旧バージョンとの互換性のために WIN32 \_が定義されています。

    また、次の前提条件が無効になっています。

    ```cpp
    #ifdef _WIN16  // 16-bit Windows code
    ...
    #else          // 32-bit Windows code
    ...
    #endif
    ```

    この場合、else 句は \_WIN32 または \_の WIN64 を表すことができます。

-   **Printf**と**wsprintf**で適切な書式指定子を使用します。

    **% P**を使用して、ポインターを16進数で印刷します。 これは、ポインターの印刷に最適な選択肢です。

    **ただし**、今後のバージョンのビジュアルC++では、データを印刷するために **% I**がサポートされる   ます。 64ビットの Windows では64ビット、32ビットの Windows では32ビットとして値が処理されます。 ビジュアルC++では、64ビットの値を出力するために **% I64**もサポートされています。

     

<!-- -->

-   アドレス空間を確認します。

    たとえば、アドレスがカーネルアドレスの場合は、その上位ビットを設定する必要があります。 最も低いシステムアドレスを取得するには、 **MM\_最も低い\_システム\_アドレス**マクロを使用します。

### <a name="pointer-arithmetic"></a>ポインターの算術演算

-   署名されていない署名付き操作を実行する場合は注意してください。

    次の点を考慮します。

    ```cpp
    ULONG x;
    LONG y;
    LONG *pVar1;
    LONG *pVar2;
     
    pVar2 = pVar1 + y * (x - 1);
    ```

    この問題が発生するのは、 *x*が符号なしであるためです。これにより、式全体が符号なしになります。 *Y*が負の値でない限り、これは成功します。 この場合、 *y*は符号なしの値に変換され、式は32ビット精度を使用して評価され、 *pVar1*に追加されます。 64ビットの Windows では、この32ビットの符号なし負の値は、大きな64ビットの正の数値になり、間違った結果が得られます。 この問題を解決するには、 *x*を符号付きの値として宣言するか、式の**LONG 型**に明示的に型キャストします。

-   16進定数と符号なしの値を使用する場合は注意してください。

    64ビットシステムでは、次のアサーションは当てはまりません。

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) == (UINT64)~(PAGE_SIZE-1)
    PAGE_SIZE = 0x1000UL  // Unsigned long - 32 bits
    PAGE_SIZE - 1 = 0x00000fff
    ```

    LHS 式:

    ```cpp
    // Unsigned expansion(UINT64)(PAGE_SIZE -1 ) = 0x0000000000000fff
    ~((UINT64)(PAGE_SIZE -1 )) = 0xfffffffffffff000
    ```

    RHS 式:

    ```cpp
    ~(PAGE_SIZE-1) = 0xfffff000
    (UINT64)(~(PAGE_SIZE - 1)) = 0x00000000fffff000
    ```

    そのため

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) != (UINT64)(~(PAGE_SIZE-1))
    ```

-   操作しないように注意してください。

    次の点を考慮します。

    ```cpp
    UINT_PTR a; ULONG b;
    a = a & ~(b - 1); 
    ```

    問題は、~ (b − 1) が 0x0000 0000 *xxxx* xxxx を生成し、0xffff ではなく0xffff が生成されること*です。* コンパイラはこれを検出しません。 この問題を解決するには、次のようにコードを変更します。

    ```cpp
    a = a & ~((UINT_PTR)b - 1);
    ```

-   バッファーサイズを計算するときは注意してください。

    次の点を考慮します。

    ```cpp
    len = ptr2 - ptr1 
    /* len could be greater than 2**32 */
    ```

    ポインター演算の**Pchar**へのポインターをキャストしています。

    **  ** *len*が**INT**または**ULONG**として宣言されている場合、コンパイラの警告が生成されます。 バッファーサイズは、正しく計算された場合でも、 **ULONG**の容量を超える可能性があります。

     

-   計算またはハードコーディングされたポインターオフセットは使用しないでください。

    構造体を使用する場合は、可能な限り[**FIELD\_OFFSET**](https://docs.microsoft.com/windows/desktop/api/ntdef/nf-ntdef-field_offset)マクロを使用して、構造体メンバーのオフセットを決定します。

-   ハードコーディングされたポインターまたはハンドル値は使用しないでください。

    **Zwの**ようなルーチンには、ハードコーディングされたポインターまたはハンドル (ハンドル) を渡さないでください。 代わりに、各プラットフォームに適切な値を持つように定義できる、無効な\_ハンドル\_値などの定数を使用します。

-   64ビットの Windows では、0xFFFFFFFF は-1 と同じではないことに注意してください。

    次に、例を示します。

    ```cpp
    DWORD index = 0;
    CHAR *p;

    // if (p[index-1] == '0') causes access violation on 64-bit Windows!
    ```

    32ビットコンピューターの場合:

    ```cpp
    p[index-1] == p[0xffffffff] == p[-1] 
    ```

    64ビットコンピューターの場合:

    ```cpp
    p[index-1] == p[0x00000000ffffffff] != p[-1]
    ```

    この問題を回避するには、*インデックス*の種類を**dword**から**dword\_PTR**に変更します。

### <a name="polymorphism"></a>多

- ポリモーフィックなインターフェイスに注意してください。

  ポリモーフィックなデータには、 **DWORD**型 (またはその他の固定精度型) のパラメーターを受け取る関数を作成しないでください。 データをポインターまたは整数値にすることができる場合、パラメーターの型は、 **DWORD**ではなく、 **\_PTR**または**pvoid**である必要があります。

  たとえば、 **DWORD**値として型指定された例外パラメーターの配列を受け取る関数は作成しないでください。 配列は、 **DWORD\_の PTR**値の配列である必要があります。 したがって、配列要素は、アドレスまたは32ビットの整数値を保持できます。 一般的な規則として、元の型が**dword**で、ポインターの幅である必要がある場合は、それを**dword\_PTR**値に変換します。 そのため、ネイティブの Win32 型に対応するポインターの有効桁数の型があります。 **DWORD**、 **ULONG**、またはその他の32ビット型をポリモーフィックな方法で使用するコードがある場合 (つまり、パラメーターまたは構造体のメンバーにアドレスを格納する場合)、現在の型の代わりに**UINT\_PTR**を使用します。

- ポインター OUT パラメーターを持つ関数を呼び出すときは注意してください。

  この操作は避けてください。

  ```cpp
  void GetBufferAddress(OUT PULONG *ptr);
  {
    *ptr=0x1000100010001000;
  }
  void foo()
  {
    ULONG bufAddress;
    //
    // This call causes memory corruption.
    //
    GetBufferAddress((PULONG *)&bufAddress);
  }
  ```

  Typecasting *bufAddress* to \* **(** ) を実行すると、コンパイラエラーが発生しません。 ただし、 *Getbufferaddress*は *& bufAddress*のメモリ位置に64ビット値を書き込みます。 *BufAddress*は32ビット値であるため、 *bufAddress*に続く32ビットは上書きされます。 これは非常にわかりにくいバグです。

- **INT**、 **LONG**、 **ULONG**、または**DWORD**にポインターをキャストしないでください。

  一部のビットのテスト、ビットの設定またはクリア、またはその他の操作を行うためにポインターをキャストする必要がある場合は、 **UINT**\_**Ptr**または**INT**\_**ptr**型を使用します。 これらの型は、32ビットと64ビットの両方の Windows のポインターのサイズに合わせてスケーリングされる整数型です (たとえば、32ビット windows の場合は**ULONG** 、64ビット windows の場合は **\_int64** )。 たとえば、次のコードを移植しているとします。

  ```cpp
  ImageBase = (PVOID)((ULONG)ImageBase | 1);
  ```

  移植プロセスの一環として、次のようにコードを変更します。

  ```cpp
  ImageBase = (PVOID)((ULONG_PTR)ImageBase | 1);
  ```

  必要に応じて、 **UINT**\_**ptr**および**INT**\_**ptr**を使用します (必須かどうか不明な場合は、大文字と小文字を区別するだけでは問題ありません)。 ポインターを型**ULONG**、 **LONG**、 **INT**、 **UINT**、または**DWORD**にキャストしないでください。

  **注** **ハンドル**は**void \\** として定義されているの<em>で、**ハンドル</em>* 値を**ULONG**値に typecasting して、下位2ビットのテスト、設定、またはクリアは、プログラミングエラーになります。

     

- ポインターを切り捨てるには、 **PtrToLong**と**PtrToUlong**を使用します。

  32ビット値へのポインターを切り捨てる必要がある場合は、 **PtrToLong**関数または**PtrToUlong**関数 ( *Basetsd*で定義されています) を使用します。 この関数は、呼び出しの間、ポインターの切り捨ての警告を無効にします。

  これらの関数は慎重に使用してください。 これらの関数のいずれかを使用してポインター変数を切り捨てると、結果として得られた**LONG**または**ULONG**がポインターにキャストされることはありません。 これらの関数は、通常はポインターによって参照されるメモリにアクセスするために必要なアドレスの上位32ビットを切り捨てます。 これらの関数を慎重に考慮せずに使用すると、コードが脆弱になります。

### <a name="data-structures-and-structure-alignment"></a>データ構造と構造体の配置

-   データ構造のポインターのすべての使用法を慎重に確認します。

    一般的なトラブル領域を次に示します。

    -   ディスクに格納されているか、32ビットプロセスと交換されるデータ構造。
    -   ポインターを持つ明示的および暗黙的な共用体。
    -   セキュリティ記述子。

<!-- -->

-   [**フィールド\_OFFSET**](https://docs.microsoft.com/windows/desktop/api/ntdef/nf-ntdef-field_offset)マクロを使用します。

    次に、例を示します。

    ```cpp
    struct xx {
       DWORD NumberOfPointers;
       PVOID Pointers[1];
    };
     
    ```

    64ビットの Windows では、次の割り当ては正しくありません。これは、コンパイラが4バイトのアラインメント要件を作成するために、構造体に追加の4バイトを埋め込むためです。

    ```cpp
    malloc(sizeof(DWORD)+100*sizeof(PVOID)); 
     
    ```

    これを正しく行う方法を次に示します。

    ```cpp
    malloc(FIELD_OFFSET(struct xx, Pointers) +100*sizeof(PVOID));
    ```

-   **型\_アラインメント**マクロを使用します。

    **型\_アラインメント**マクロは、現在のプラットフォームの特定のデータ型のアラインメント要件を返します。 次に、例を示します。

    ```cpp
    TYPE_ALIGNMENT(KFLOATING_SAVE) == 4 on x86, 8 on Itanium
    TYPE_ALIGNMENT(UCHAR) == 1 everywhere
    ```

    例として、次のようなコードがあります。

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, sizeof(ULONG));
    ```

    次のように変更すると、移植性が高くなります。

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, TYPE_ALIGNMENT(ULONG));
    ```

-   パブリックカーネル構造でのデータ型の変更を監視します。

    たとえば、IO\_状態\_ブロック構造の**情報**フィールドの型が**ULONG\_PTR**になっています。

-   Structure パッキングディレクティブを使用する場合は注意が必要です。

    64ビットの Windows では、データ構造が不整合になっている場合、 [**Rtlcopymemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcopymemory)や**memcpy**などの構造を操作するルーチンではエラーは発生しません。 代わりに、例外が発生します。 次に、例を示します。

    ```cpp
    #pragma pack (1)  /* also set by /Zp switch */
    struct Buffer {
        ULONG size;
        void *ptr;
    };

    void SetPointer(void *p) {
        struct Buffer s;
        s.ptr = p;  /* will cause alignment fault */
        ...
    }
    ```

    この問題を解決するには、**整列**されていないマクロを使用します。

    ```cpp
    void SetPointer(void *p) {
        struct Buffer s;
        *(UNALIGNED void *)&s.ptr = p;
    }
    ```

    残念ながら、Itanium ベースのプロセッサでは、**整列**されていないマクロを使用すると非常にコストが高くなります。 より適切な解決策は、構造体の先頭に64ビットの値とポインターを配置することです。

    **注**  可能であれば、同じヘッダーファイルで異なるパッキングレベルを使用しないようにしてください。

     

### <a name="additional-information"></a>追加情報

-   [64ビットドライバーでの32ビット i/o のサポート](supporting-32-bit-i-o-in-your-64-bit-driver.md)

-   [64 ビット版 Windows の準備](https://docs.microsoft.com/windows/desktop/WinProg64/getting-ready-for-64-bit-windows)(ユーザーモードアプリケーション移植ガイド)

 

 




