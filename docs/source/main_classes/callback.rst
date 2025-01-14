Callbacks
-----------------------------------------------------------------------------------------------------------------------

Callbacks are objects that can customize the behavior of the training loop in the PyTorch
:class:`~transformers.Trainer` (this feature is not yet implemented in TensorFlow) that can inspect the training loop
state (for progress reporting, logging on TensorBoard or other ML platforms...) and take decisions (like early
stopping).

Callbacks are "read only" pieces of code, apart from the :class:`~transformers.TrainerControl` object they return, they
cannot change anything in the training loop. For customizations that require changes in the training loop, you should
subclass :class:`~transformers.Trainer` and override the methods you need (see :doc:`trainer` for examples).

By default a :class:`~transformers.Trainer` will use the following callbacks:

- :class:`~transformers.DefaultFlowCallback` which handles the default behavior for logging, saving and evaluation.
- :class:`~transformers.PrinterCallback` or :class:`~transformers.ProrgressCallback` to display progress and print the
  logs (the first one is used if you deactivate tqdm through the :class:`~transformers.TrainingArguments`, otherwise
  it's the second one).
- :class:`~transformers.integrations.TensorBoardCallback` if tensorboard is accessible (either through PyTorch >= 1.4
  or tensorboardX).
- :class:`~transformers.integrations.WandbCallback` if `wandb <https://www.wandb.com/>`__ is installed.
- :class:`~transformers.integrations.CometCallback` if `comet_ml <https://www.comet.ml/site/>`__ is installed.
- :class:`~transformers.integrations.MLflowCallback` if `mlflow <https://www.mlflow.org/>`__ is installed.

The main class that implements callbacks is :class:`~transformers.TrainerCallback`. It gets the
:class:`~transformers.TrainingArguments` used to instantiate the :class:`~transformers.Trainer`, can access that
Trainer's internal state via :class:`~transformers.TrainerState`, and can take some actions on the training loop via
:class:`~transformers.TrainerControl`.


Available Callbacks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here is the list of the available :class:`~transformers.TrainerCallback` in the library:

.. autoclass:: transformers.integrations.CometCallback
    :members: setup

.. autoclass:: transformers.DefaultFlowCallback

.. autoclass:: transformers.PrinterCallback

.. autoclass:: transformers.ProgressCallback

.. autoclass:: transformers.integrations.TensorBoardCallback

.. autoclass:: transformers.integrations.WandbCallback
    :members: setup

.. autoclass:: transformers.integrations.MLflowCallback
    :members: setup


TrainerCallback
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.TrainerCallback
    :members:


TrainerState
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.TrainerState
    :members:


TrainerControl
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.TrainerControl
    :members:
