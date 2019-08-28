
Selection of Training, Guard cells and offset.

The number of Training Cells in both the dimensions.
Tr=10;
Td=8;

The number of Guard Cells in both dimensions around the Cell under test:
Gr=4;
Gd=4;

 offset the threshold by SNR value in dB
offset=6;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

Implementation steps for the 2D CFAR process.

Determine the number of Training cells for each dimension. Similarly, pick the number of guard cells.
Slide the cell under test across the complete matrix. Make sure the CUT has margin for Training and Guard cells from the edges.
For every iteration sum the signal level within all the training cells. 
Average the summed values for all of the training cells used.
Further add the offset to it to determine the threshold.
Next, compare the signal under CUT against this threshold.
If the CUT level > threshold assign it a value of 1, else equate it to 0.


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Steps taken to suppress the non-thresholded cells at the edges:

a) Make The default value of the thresholded_output = zero as follows:

thresholded_output=zeros(size(RDM));

b) compare only the cells under test to threshold and if they exceed the threshold, set the value to 1

        CUT=RDM(i,j);
        if(CUT<threshold)
            thresholded_output(i,j)=0;
        else
            thresholded_output(i,j)=1;