```kotlin[1-3|5-9|11-21]
enum CardNetwork {
    VISA, MASTERCARD
}

class CreditCardIdentifier {
    fun getCreditNetwork(number: String): CardNetwork? 
        = TODO("use some crazy regex that would usually"
            + "be implemented for each platform") 
}

class CreditCardIdentifierTest {
    private val testMe = CreditCardIdentifier() 

    @Test
    fun creditCardType_Visa() {
        assertEquals(
            CardNetwork.VISA, 
            testMe.getCreditNetwork("4111")
        )
    }
}
```