# Описание переходов и возможных состояний

Для улучшения в первую очередь моего же понимания, в таблицу добавлена колонка "Шаг", куда будет вписываться транзакция (из списка в предыдущем задании), результатом которой стало возникновение текущего события и смена состояния.

Рефанд в данном случае описан в довольно упрощенном виде, так как он может технически не быть частью данной саги, а отдельным процессом, к тому же к нему нет требований, помимо необходимости избегать его насколько возможно.

| Исходное состояние | Переходное состояние | Событие | Шаг |
| --- | --- | --- | --- |
| - | Created | TransactionCreated | CREATE_PAYMENT |
| Created | FundsReserved | FundsReservedSuccessfully | RESERVE_FUNDS |
| FundsReserved | SecurityCheckPending | SentForFraudCheck | FRAUD_CHECK |
| SecurityCheckPending | Allowed | FraudCheckSuccess | FRAUD_CHECK |
| Allowed | Complete | TransactionCompleted | PAYMENT_TRANSFER |
| Created | ReservationFailed | FundsFailedToBeReserved | RESERVE_FUNDS |
| SecurityCheckPending | ManualReview | SentForManualReview | FRAUD_CHECK |
| SecurityCheckPending | Declined | FraudCheckFailed | FRAUD_CHECK |
| ManualReview | Allowed | FraudCheckSuccess | FRAUD_CHECK |
| ManualReview | Declined | FraudCheckFailed | FRAUD_CHECK |
| ManualReview | Allowed | ManualReviewHasTimedOut | FRAUD_CHECK |
| Declined | ReservationReleased | ReservationReleased | RELEASE_RESERVED_FUNDS |
| ReservationReleased | Cancelled | TransactionCancelled | CANCEL_PAYMENT |
| Complete | Refunded | RefundRequested | REFUND_PAYMENT |
