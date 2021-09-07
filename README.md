# lstm_stock_market_prediction
Statements

- Between training and validation samples need to be 1 year gap

- Forward-chaining cross-validation with 1 year step and two year lookback period will be used.

- Each tradingitemid sequence need to be splited to n samples, where n - it's number of observations of tradingitemid

- Validation dataset in keras training process will have one target for each tradingitemid. And all timestamps features of one tradingitemid are combined to one sequence. This trick is used only to speedup validation inference. For final model validation all targets will be used.

- train_generator produces all samples, while test_generator_fast produces one sample for each tradingitemid

- No zero padding will be used, batch size will be equal to 1

Alternatives:

Zero padding will be used in batch generator, batch size will be equal to m
No zero padding will be used, batch size will be equal to m. For each batch need to be generated sequences of the same length
The final predictions will be based on average prediction, based on k models, where k - is number of folds in cross validation.

Train generator example:

tradingitemid: [1, 2, 3, 4, 5] -> [1, 0, 1, 0, 1]

[1] -> [1]

[1, 2] -> [0]

[1, 2, 3] -> [1]

[1, 2, 3, 4] -> [0]

[1, 2, 3, 4, 5] -> [1]

Test generator fast example:

tradingitemid: [1, 2, 3, 4, 5] -> [1, 0, 1, 0, 1]

[1, 2, 3, 4, 5] - > [1]
